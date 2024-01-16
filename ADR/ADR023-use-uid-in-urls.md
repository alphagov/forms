# ADR23: Use UIDs in URLs to replace form-id

Date: 08/01/24

## Status
Accepted

## Context

See this spike for details about the required changes https://trello.com/c/BruuEN5Z/1225-spike-change-ids-in-urls-of-forms-to-not-be-the-primary-key

We need to switch away from putting database ids in our URLs. Currently, form urls look something like this:
`https://submit.forms.service.gov.uk/form/1234/apply-for-an-apple/5678`

Where `1234` is the form-id.

We instead want to change our URLs so that they look like this: 

`https://submit.forms.service.gov.uk/form/51f5b6f7/apply-for-an-apple/5678`

where the 8 char hex code `51f5b6f7` has replaced the form-id.

We also have to handle existing form URLs, and how we want to maintain them.

In order to achieve this change, we'll add an `external_id` to all of our forms, which will be used to identify from the exterior of the API. For pre-existing live forms, they will be given their current `id` as their `external_id` which will maintain their current URLs as a result. 

For example, a new form will have it's `external_id` as `51f5b6f7` whereas an old form will use it's current `id` of `1234` as its `external_id`. 

## Decision

We will be using an external ID to retrieve forms from forms-api

## Consequences

URLs will no longer expose our database primary key IDs, and our API will not find objects by their primary key ID. Instead, their external ID will need to be used. 

URLs for forms-runner and forms-admin will use the external ID, which will change their appearance. 
