# ADR044: Translate API response at request time

Date: 2025-08-01

## Status

Accepted

## Context

Our current API is based around form documents which contain all the information forms-runner needs to render a form:

```jsonc
{
  "form_id": "7",
  "name": "A form for testing file upload",
  "submission_email": "david.biddle@digital.cabinet-office.gov.uk",
  "privacy_policy_url": null,
  "form_slug": "a-form-for-testing-file-upload",
  "support_email": null,
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": null,
  "question_section_completed": false,
  "declaration_section_completed": false,
  "created_at": "2025-03-27T12:05:49.395300Z",
  "updated_at": "2025-07-29T14:35:44.423406Z",
  "creator_id": 1,
  "what_happens_next_markdown": null,
  "payment_url": null,
  "submission_type": "email",
  "share_preview_completed": false,
  "s3_bucket_name": null,
  "s3_bucket_aws_account_id": null,
  "s3_bucket_region": null,
  "start_page": 33,
  "steps": [
    {
      "id": 33,
      "position": 1,
      "next_step_id": null,
      "type": "question_page",
      "data": {
        "question_text": "Upload your file",
        "hint_text": "",
        "answer_type": "file",
        "is_optional": false,
        "answer_settings": null,
        "page_heading": "Annual report",
        "guidance_markdown": "Some guidance",
        "is_repeatable": false
      },
      "routing_conditions": []
    }
  ]
}
```

A form can have multiple from documents associated with it, depending on its state:

```jsonc
{
  "id": "7",
  "links": {
    "self": "/api/v2/forms/7",
    "draft": "/api/v2/forms/7/draft",
    "live": "/api/v2/forms/7/live",
    // or
    "archived": "/api/v2/forms/7/archived"
  }
}
```

Currently form documents only contain English language text, but we want to add Welsh translations for form-filler facing text.

There are a few ways we could model this.

### 1. Adding additional fields to the form document

One option is to add extra keys to the existing form document with the new translations. We could do this by renaming the existing field with an `_en` suffix and adding a new key with a `_cy` suffix. This is roughly what the mobility gem does with its database columns:

```jsonc
{
  "form_id": "7",
  "name_en": "A form for testing file upload",
  "name_cy": "Ffurflen ar gyfer profi uwchlwytho ffeiliau",
  "submission_email": "david.biddle@digital.cabinet-office.gov.uk",
  "privacy_policy_url": null,
  "form_slug": "a-form-for-testing-file-upload",
  "support_email": null,
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": null,
  "question_section_completed": false,
  "declaration_section_completed": false,
  "created_at": "2025-03-27T12:05:49.395300Z",
  "updated_at": "2025-07-29T14:35:44.423406Z",
  "creator_id": 1,
  "what_happens_next_markdown": null,
  "payment_url": null,
  "submission_type": "email",
  "share_preview_completed": false,
  "s3_bucket_name": null,
  "s3_bucket_aws_account_id": null,
  "s3_bucket_region": null,
  "start_page": 33,
  "steps": [
    {
      "id": 33,
      "position": 1,
      "next_step_id": null,
      "type": "question_page",
      "data": {
        "question_text_en": "Upload your file",
        "question_text_cy": "Llwythwch eich ffeil i fyny",
        "hint_text": "",
        "answer_type": "file",
        "is_optional": false,
        "answer_settings": null,
        "page_heading_en": "Annual report",
        "page_heading_cy": "Adroddiad blynyddol",
        "guidance_markdown_en": "Some guidance",
        "guidance_markdown_cy": "Peth arweiniad",
        "is_repeatable": false
      },
      "routing_conditions": []
    }
  ]
}
```

We could also keep the existing keys as they are, and add a new 'translations' object containing only the Welsh translations for the relevant field:

```jsonc
// or:
{
  "form_id": "7",
  "name": "A form for testing file upload",
  "submission_email": "david.biddle@digital.cabinet-office.gov.uk",
  "privacy_policy_url": null,
  "form_slug": "a-form-for-testing-file-upload",
  "support_email": null,
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": null,
  "question_section_completed": false,
  "declaration_section_completed": false,
  "created_at": "2025-03-27T12:05:49.395300Z",
  "updated_at": "2025-07-29T14:35:44.423406Z",
  "creator_id": 1,
  "what_happens_next_markdown": null,
  "payment_url": null,
  "submission_type": "email",
  "share_preview_completed": false,
  "s3_bucket_name": null,
  "s3_bucket_aws_account_id": null,
  "s3_bucket_region": null,
  "start_page": 33,
  "translations": {
    "cy": {
      "name": "Ffurflen ar gyfer profi uwchlwytho ffeiliau"
    }
  },
  "steps": [
    {
      "id": 33,
      "position": 1,
      "next_step_id": null,
      "type": "question_page",
      "data": {
        "question_text": "Upload your file",
        "hint_text": "",
        "answer_type": "file",
        "is_optional": false,
        "answer_settings": null,
        "page_heading": "Annual report",
        "guidance_markdown": "Some guidance",
        "is_repeatable": false
      },
      "translations": {
        "cy": {
          "question_text": "Llwythwch eich ffeil i fyny",
          "page_heading": "Adroddiad blynyddol",
          "guidance_markdown": "Peth arweiniad"
        }
      },
      "routing_conditions": []
    }
  ]
}
```

Or with translated fields stored as objects (as proposed in the unimplemented [ADR007: Store form text data as objects](ADR007-store-form-text-data-as-objects.md))

```jsonc
{
  "form_id": "7",
  "name": {
    "en": "A form for testing file upload",
    "cy": "Ffurflen ar gyfer profi uwchlwytho ffeiliau"
  },
  "submission_email": "david.biddle@digital.cabinet-office.gov.uk",
  "privacy_policy_url": null,
  "form_slug": "a-form-for-testing-file-upload",
  "support_email": null,
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": null,
  "question_section_completed": false,
  "declaration_section_completed": false,
  "created_at": "2025-03-27T12:05:49.395300Z",
  "updated_at": "2025-07-29T14:35:44.423406Z",
  "creator_id": 1,
  "what_happens_next_markdown": null,
  "payment_url": null,
  "submission_type": "email",
  "share_preview_completed": false,
  "s3_bucket_name": null,
  "s3_bucket_aws_account_id": null,
  "s3_bucket_region": null,
  "start_page": 33,
  "steps": [
    {
      "id": 33,
      "position": 1,
      "next_step_id": null,
      "type": "question_page",
      "data": {
        "question_text": {
          "en": "Upload your file",
          "cy": "Llwythwch eich ffeil i fyny"
        },
        "hint_text": "",
        "answer_type": "file",
        "is_optional": false,
        "answer_settings": null,
        "page_heading": {
          "en": "Annual report",
          "cy": "Adroddiad blynyddol"
        },
        "guidance_markdown": {
          "en": "Some guidance",
          "cy": "Peth arweiniad"
        },
        "is_repeatable": false
      },
      "routing_conditions": []
    }
  ]
}
```

These cases are essentially the same in how forms-runner deals with them.
Benefits:

- Few admin/api changes required
  Disadvantages:
- More runner logic, since we'd have to manage choosing the right translation and fallback behaviour in runner.
- We'd get less benefit from the Mobility gem - we'd be using it for managing the columns and dealing with translations in admin, but we wouldn't be using its querying or fallback features in forms-runner.
- For forms with lots of content (e.g. multiple pages with a large amount of detailed guidance or what happens next text), this would increase the size of the request quite a lot since this information would be present in two different languages. Much of that content wouldn't be used for a given request, since the runner only shows one language at a time.
- Additional languages would make it even more verbose.

### 2. Selecting languages at request time

In this approach, we would allow the runner to request a specific language when requesting the form from the API, and the API would only supply translations for the requested language.

So `/forms/7/live?language=en` would return:

```jsonc
{
  "form_id": "7",
  "name": "A form for testing file upload",
  "submission_email": "david.biddle@digital.cabinet-office.gov.uk",
  "privacy_policy_url": null,
  "form_slug": "a-form-for-testing-file-upload",
  "support_email": null,
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": null,
  "question_section_completed": false,
  "declaration_section_completed": false,
  "created_at": "2025-03-27T12:05:49.395300Z",
  "updated_at": "2025-07-29T14:35:44.423406Z",
  "creator_id": 1,
  "what_happens_next_markdown": null,
  "payment_url": null,
  "submission_type": "email",
  "share_preview_completed": false,
  "s3_bucket_name": null,
  "s3_bucket_aws_account_id": null,
  "s3_bucket_region": null,
  "language": "en",
  "available_languages": ["en", "cy"],
  "start_page": 33,
  "steps": [
    {
      "id": 33,
      "position": 1,
      "next_step_id": null,
      "type": "question_page",
      "data": {
        "question_text": "Upload your file",
        "hint_text": "",
        "answer_type": "file",
        "is_optional": false,
        "answer_settings": null,
        "page_heading": "Annual report",
        "guidance_markdown": "Some guidance",
        "is_repeatable": false
      },
      "routing_conditions": []
    }
  ]
}
```

And `/forms/7/live?language=cy`, would return the same object with any Welsh translations overwriting the English:

```jsonc
{
  "form_id": "7",
  "name": "Ffurflen ar gyfer profi uwchlwytho ffeiliau",
  "submission_email": "david.biddle@digital.cabinet-office.gov.uk",
  "privacy_policy_url": null,
  "form_slug": "a-form-for-testing-file-upload",
  "support_email": null,
  "support_phone": null,
  "support_url": null,
  "support_url_text": null,
  "declaration_text": null,
  "question_section_completed": false,
  "declaration_section_completed": false,
  "created_at": "2025-03-27T12:05:49.395300Z",
  "updated_at": "2025-07-29T14:35:44.423406Z",
  "creator_id": 1,
  "what_happens_next_markdown": null,
  "payment_url": null,
  "submission_type": "email",
  "share_preview_completed": false,
  "s3_bucket_name": null,
  "s3_bucket_aws_account_id": null,
  "s3_bucket_region": null,
  "language": "cy",
  "available_languages": ["en", "cy"],
  "start_page": 33,
  "steps": [
    {
      "id": 33,
      "position": 1,
      "next_step_id": null,
      "type": "question_page",
      "data": {
        "question_text": "Llwythwch eich ffeil i fyny",
        "hint_text": "",
        "answer_type": "file",
        "is_optional": false,
        "answer_settings": null,
        "page_heading": "Adroddiad blynyddol",
        "guidance_markdown": "Peth arweiniad",
        "is_repeatable": false
      },
      "routing_conditions": []
    }
  ]
}
```

Note that in this case we would still need to store the individual translations in the form document JSON. We could use one of the formats described in option 1 for this.

Without the query string it should return the whole form document, including translations for all languages. We think forms-admin will need this.

If the runner requests a language which is not in the `available_languages` array, the API should return an error.

Advantages:

- Request size doesn't increase
- Allows us to customise anything to a locale, without having to implement a new locale specific attribute in the API schema
- Keeps the translation logic out of runner

Disadvantages:

- Requires more logic in the API to choose the right translation - we already have some conversion logic, but we're currently trying to reduce the amount of logic in this repo.
- API is doing more work at request time, which might slow down its responses for forms with lots of questions.
- Small runner change required to request the correct version
- we'd have two separate schemas - one for storage, and one for the resource provided to forms-runner.

### 3. Creating separate Welsh and English snapshots when making a form live

We could create separate snapshots for Welsh and English when making a form live - so the API would store two separate form documents, one in English and one in Welsh. At request time, the runner would request a form document and request a language, and API would return the relevant version of the form document. The objects returned would be identical to those in the 'Selecting languages at request time' approach. The difference would be that the form resources are stored separately in the forms-api rather than converted at request time from a single form resource.

Advantages:

- API structure doesn't change aside from the addition of a query parameter. Allows us to customise any field to a locale in future, without having to implement a new locale specific attribute in the schema
- All translation logic including fallbacks can be handled within admin, API/runner don't have to do any processing on the resulting form documents - just need to serve/request the right version.
- No additional processing or conversion would be required at request time, just returning an existing form document.
- Reduces the amount of code we'll have to move if we merge forms-api into forms-admin.

Disadvantages:

- More complexity in forms-admin.
- Potential for overlap with API team's work.
- Small runner change required to request the correct version.
- Having two separate documents might risk the two versions going out of sync unexpectedly, but we should be able to manage the risk of this.

## Decision

We will implement the 'Creating separate Welsh and English snapshots when making a form live' pattern.

## Consequences

Changes to forms-runner should be minimal, limited to making a request for the correct locale.

We'll need to do some extra work in forms-admin and forms-api to make it possible to save multiple form resources in different languages for the same form.
