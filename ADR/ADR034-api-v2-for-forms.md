# ADR034: API v2 for Forms

Date: 2024-08-19

## Status

Accepted

## Context

Currently forms are modelled in the forms-api app, not the forms-admin app, however the forms-admin does most of the work manipulating forms. This slows down development when we need to make changes to how forms are represented, such as when we want to add new features.

## Decision

We've decided to create a new set of API endpoints in the forms-api app with a simpler interface, and move the form model.

## Consequences

- developers will be able to make more changes to forms-admin without having to also change forms-api
- forms-api will be simpler
- form objects will not be validated by forms-api

## Appendix: Original request for comment

Below is reproduced the RFC that was shared with the team to help make this decision:

### Introduction

Design goals:

- Allow moving model logic from forms-api to forms-admin
- Change building block of forms from pages to steps
- Improve developer experience when making changes to form schema

Non-goals:

- Changing API endpoints unrelated to forms/pages
- Supporting external consumers

Design considerations:

- Treat forms as opaque JSON documents
- No endpoints for pages/conditions etc, wire format is basically just form snapshot
- Form is made up of steps as per https://github.com/alphagov/forms/discussions/174
- No validation of form steps (?)
- Better handling of live/draft/archived (?)
- Don’t use ActiveResource (?)

What does that unlock?

Can move functionality from api to admin incrementally (?)
Steps abstraction makes JSON document structure less complex (?)
Eventually less duplication of code between API and admin, more responsive admin app

### Future directions

The aim of these changes is to enable future changes, rather than being an ideal endpoint.

This RFC tries to support any of the following future changes to the forms-api app:

- Replacing with off the shelf document storage
- Merging with forms-admin
- Adding OpenAPI schema validation
- Anything else…?

### v2 API for forms

This RFC proposes changing the API presented by forms-api, specifically the part of the API related to forms. Other parts of the API in forms-api or in other apps are outside the scope of this ADR.

#### Form endpoints

The current endpoints related to forms `/api/v1/forms*` will be deprecated. The following endpoints will be added:

```javascript
Verbs                       URI pattern

GET,POST                    /api/v2/forms
GET                         /api/v2/forms/:id
GET,PATCH,PUT,DELETE        /api/v2/forms/:id/draft
GET,PATCH,PUT,DELETE        /api/v2/forms/:id/live
GET,PATCH,PUT,DELETE        /api/v2/forms/:id/archived
```

#### Form/forms response

The response for a form or array of forms has been simplified so that it contains only links to draft, live, or archived form documents. The task statuses and form statuses should be the responsibility of forms-admin rather than forms-api.

It is expected that as part of moving logic to forms-admin the forms-admin database will have its own collection of form records, so that forms-admin will usually make queries to its own database rather than querying forms-api.

```javascript
GET /api/v2/forms HTTP/1.1

HTTP/1.1 200 OK

[
  {
    "id": "2338n9ko",
    "links": {
      "self": "https://api.forms.service.gov.uk/forms/2338n9ko",
      "draft": "https://api.forms.service.gov.uk/forms/2338n9ko/draft",
      "live": "https://api.forms.service.gov.uk/forms/2338n9ko/live",
    },
  },
  {
    "id": "xknjdqdh",
    "links": {
      "self": "https://api.forms.service.gov.uk/forms/xknjdqdh",
      "archived": "https://api.forms.service.gov.uk/forms/xknjdqdh/archived",
    },
  },
]
```

#### Form document response

A form document is a JSON object that describes a form sufficiently for it to be rendered by forms-runner. The `/draft`, `/live` and `archived` endpoints all return a form document both currently in the v1 API and in the proposed v2 API.

The v2 API form document has some changes from the v1 API response, corresponding to the changes proposed in option 1 of the [discussion on the add another answer data model](https://github.com/alphagov/forms/discussions/174). These changes are backwards incompatible and so require a new API version. The main change is that the form now has a `steps` attribute which is a collection of `steps`, with each `step` containing `question` data. The `steps` attribute replaces the `pages` attribute.

```javascript
GET /api/v2/forms/8/live HTTP/1.1

HTTP/1.1 200 OK

{
  "id": 8,
  "name": "capybara test form 2024-08-02 11:54.00",
  "submission_email": "govuk-forms-automation-tests@digital.cabinet-office.gov.uk",
  "privacy_policy_url": "https://www.gov.uk/help/privacy-notice",
  "form_slug": "capybara-test-form-2024-08-02-11-54-00",
  "support_email": "govuk-forms-automation-tests@digital.cabinet-office.gov.uk",
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": "",
  "question_section_completed": true,
  "declaration_section_completed": true,
  "created_at": "2024-08-02T08:54:03.277Z",
  "updated_at": "2024-08-02T08:54:12.905Z",
  "creator_id": 1,
  "organisation_id": 1,
  "what_happens_next_markdown": "We'll send you an email to let you know the outcome. You'll usually get a response within 10 working days.",
  "payment_url": null,
  "start_page": 18,
  "steps": [
    {
      "id": 18,
      "next_step_id": 19,
      "created_at": "2024-08-02T08:54:04.908Z",
      "updated_at": "2024-08-02T08:54:04.908Z",
      "form_id": 8,
      "position": 1,
      "type": "Question",
      "data": {
        "question_text": "Do you want to remain anonymous?",
        "hint_text": "",
        "answer_type": "selection",
        "is_optional": false,
        "answer_settings": {
          "only_one_option": "true",
          "selection_options": [
            {
              "name": "Yes"
            },
            {
              "name": "No"
            }
          ]
        },
        "page_heading": null,
        "guidance_markdown": null,
        "is_repeatable": false
      },
      "routing_conditions": [
        {
          "id": 3,
          "check_step_id": 18,
          "routing_step_id": 18,
          "goto_step_id": null,
          "answer_value": "Yes",
          "created_at": "2024-08-02T08:54:07.479Z",
          "updated_at": "2024-08-02T08:54:07.479Z",
          "skip_to_end": true,
          "validation_errors": []
        }
      ]
    },
    {
      "id": 19,
      "next_step_id": null,
      "created_at": "2024-08-02T08:54:06.227Z",
      "updated_at": "2024-08-02T08:54:06.227Z",
      "form_id": 8,
      "position": 2,
      "type": "Question",
      "data": {
        "question_text": "What is your name?",
        "hint_text": "",
        "answer_type": "text",
        "is_optional": false,
        "answer_settings": {
          "input_type": "single_line"
        },
        "page_heading": null,
        "guidance_markdown": null,
        "is_repeatable": false,
      },
      "routing_conditions": []
    }
  ],
  "live_at": "2024-08-02T08:54:12.905Z"
}
```

### Using the API

To list forms stored in the API the client should make a `GET` request to `/api/v2/forms`.

To see the state of a particular form the client can either search the response to the above call, or make a `GET` request to `/api/v2/forms/:form_id`, where `:form_id` is one of the `id`s listed in the above response.

To retrieve the details of a form the client follows one of the `links` in the above response, making a `GET` request to `/api/v2/forms/:form_id/:state`, where `:state` (draft, live, or archived) is the key to one of the links and represents the state of the form in the requested form document.

To create a new form the client must make a `POST` request to `/api/v2/forms` with the `id` of the new form. The client may then make a `PUT` request to `/api/v2/forms/:form_id/draft` to assign the attributes of the new form. When the form is edited the client should use a `PUT` or `PATCH` request to the `draft` endpoint to update the document.

To make a form live the client must make a `PUT` request to `/api/v2/forms/:form_id/live` with the form document that they want to be live. The client may also make a `DELETE` request to `api/v2/forms/:form_id/draft` to indicate that the form has not had changes made to the draft since being made live.
To archive a form the client must make a `PUT` request to `/api/v2/forms/:form_id/archived` with the form document that was live. The client must then make a `DELETE` request to `/api/v2/forms/:form_id/live` to stop the live form document from being accessed.

When changes are made to a live or archived form, the client must make a `PUT` request to `/api/v2/forms/:form_id/draft` with the form document that was live or archive plus the changes.

Note that the form document endpoints do not represent or enforce the transitions of a form lifecycle. It is expected that as part of moving logic from forms-api to forms-admin the forms-admin app will need to manage the form lifecycle state machine itself, so it is not needed in forms-api. Instead the v2 API is designed to be similar to a document or object storage system.

## Migration path

Create v2 GET endpoints which serves existing data with some minor transformations

Update runner to use v2 endpoints only

Create a new table for holding form documents. Changes using v1 endpoints should update the form document table. Changes using v2 endpoints should update records for v1 endpoints.

Start copying code for validating questions/pages from forms-api to forms-admin. Change admin to update using v2 endpoints when changing questions/pages.

Remove pages controllers and models from forms-api.

Do not start implementing question sets until v1 api for questions/pages is removed from forms-api.

# Appendix

## v1 API for forms

### Form endpoints

```javascript
Verbs                       URI pattern

GET,POST              /api/v1/forms
GET,PATCH,PUT,DELETE  /api/v1/forms/:id
GET                   /api/v1/forms/:id/draft
GET                   /api/v1/forms/:id/live
GET                   /api/v1/forms/:id/archived
POST                  /api/v1/forms/:id/make-live
POST                  /api/v1/forms/:id/archive
PATCH                 /api/v1/forms/update-organisation-for-creator
GET,POST              /api/v1/forms/:form_id/pages/:page_id/conditions
GET,PATCH,PUT,DELETE  /api/v1/forms/:form_id/pages/:page_id/conditions/:condition_id
GET,POST              /api/v1/forms/:form_id/pages
GET,PATCH,PUT,DELETE  /api/v1/forms/:form_id/pages/:page_id
PUT                   /api/v1/forms/:form_id/pages/:page_id/down
PUT                   /api/v1/forms/:form_id/pages/:page_id/up
```

### Form/forms response

```javascript
GET /api/v1/forms/8 HTTP/1.1

HTTP/1.1 200 OK

{
  "id": 8,
  "name": "capybara test form 2024-08-02 11:54.00",
  "submission_email": "govuk-forms-automation-tests@digital.cabinet-office.gov.uk",
  "privacy_policy_url": "https://www.gov.uk/help/privacy-notice",
  "form_slug": "capybara-test-form-2024-08-02-11-54-00",
  "support_email": "govuk-forms-automation-tests@digital.cabinet-office.gov.uk",
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": "",
  "question_section_completed": true,
  "declaration_section_completed": true,
  "created_at": "2024-08-02T08:54:03.277Z",
  "updated_at": "2024-08-02T08:54:12.905Z",
  "creator_id": 1,
  "organisation_id": 1,
  "what_happens_next_markdown": "We'll send you an email to let you know the outcome. You'll usually get a response within 10 working days.",
  "state": "live",
  "payment_url": null,
  "live_at": "2024-08-02T08:54:12.905Z",
  "start_page": 18,
  "has_draft_version": false,
  "has_live_version": true,
  "has_routing_errors": false,
  "ready_for_live": true,
  "incomplete_tasks": [],
  "task_statuses": {
    "name_status": "completed",
    "pages_status": "completed",
    "declaration_status": "completed",
    "what_happens_next_status": "completed",
    "payment_link_status": "optional",
    "privacy_policy_status": "completed",
    "support_contact_details_status": "completed",
    "make_live_status": "completed"
  }
}
```

### Form document response

```javascript
GET /api/v1/forms/8/live HTTP/1.1

HTTP/1.1 200 OK

{
  "id": 8,
  "name": "capybara test form 2024-08-02 11:54.00",
  "submission_email": "govuk-forms-automation-tests@digital.cabinet-office.gov.uk",
  "privacy_policy_url": "https://www.gov.uk/help/privacy-notice",
  "form_slug": "capybara-test-form-2024-08-02-11-54-00",
  "support_email": "govuk-forms-automation-tests@digital.cabinet-office.gov.uk",
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": "",
  "question_section_completed": true,
  "declaration_section_completed": true,
  "created_at": "2024-08-02T08:54:03.277Z",
  "updated_at": "2024-08-02T08:54:12.905Z",
  "creator_id": 1,
  "organisation_id": 1,
  "what_happens_next_markdown": "We'll send you an email to let you know the outcome. You'll usually get a response within 10 working days.",
  "payment_url": null,
  "start_page": 18,
  "pages": [
    {
      "id": 18,
      "next_page": 19,
      "created_at": "2024-08-02T08:54:04.908Z",
      "updated_at": "2024-08-02T08:54:04.908Z",
      "form_id": 8,
      "position": 1,
      "question_text": "Do you want to remain anonymous?",
      "hint_text": "",
      "answer_type": "selection",
      "is_optional": false,
      "answer_settings": {
        "only_one_option": "true",
        "selection_options": [
          {
            "name": "Yes"
          },
          {
            "name": "No"
          }
        ]
      },
      "page_heading": null,
      "guidance_markdown": null,
      "is_repeatable": false,
      "routing_conditions": [
        {
          "id": 3,
          "check_page_id": 18,
          "routing_page_id": 18,
          "goto_page_id": null,
          "answer_value": "Yes",
          "created_at": "2024-08-02T08:54:07.479Z",
          "updated_at": "2024-08-02T08:54:07.479Z",
          "skip_to_end": true,
          "validation_errors": []
        }
      ]
    },
    {
      "id": 19,
      "next_page": null,
      "created_at": "2024-08-02T08:54:06.227Z",
      "updated_at": "2024-08-02T08:54:06.227Z",
      "form_id": 8,
      "position": 2,
      "question_text": "What is your name?",
      "hint_text": "",
      "answer_type": "text",
      "is_optional": false,
      "answer_settings": {
        "input_type": "single_line"
      },
      "page_heading": null,
      "guidance_markdown": null,
      "is_repeatable": false,
      "routing_conditions": []
    }
  ],
  "live_at": "2024-08-02T08:54:12.905Z"
}
```

