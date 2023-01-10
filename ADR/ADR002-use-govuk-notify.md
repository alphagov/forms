# ADR002: Use GOV.UK Notify

Date: 2022-04-07

## Status

Superseded

## Context

The initial delivery mechanism of GOV.UK Forms submissions will be via email to the form processors. Additionally, to begin with we will be tackling more simple forms, notably ones without additional supporting documents being required on submission (e.g. attaching a photo).

For people filling in the forms we require a way to send them confirmation emails that their answers were submitted.

These requirements mean we need a way of sending emails to any email address with multiple different formats, though attachments are optional to begin with.

The approaches possible consist of using GOV.UK Notify, Amazon SES, or other similar platforms.

## Decision

We have decided to use GOV.UK Notify to send emails to our users for the following reasons
- It's readily used within government
- It has the features we require for early on in our private beta
- Easy to integrate with

## Consequences

As a result of this decision, we will need to create a live GOV.UK Notify account and then in the future we can integrate with this to send our emails.

However, things we need to keep in mind as we go through private beta and will need to investigate in the future, for example:

- GOV.UK Notify does not support email attachments, we will need to consider how best manage file uploads and whether or not direct email attachments will be required when those forms are being worked on for the platform.
- GOV.UK Notify does not support adding reply-to email addresses over the API, though you can specify them per email if they've been added in the web UI.
  - There are workarounds possible for this, however as we scale these will be less realistic and being able to add them over the API by the user would be required.
- Data sent in the emails will be stored for 7 days, this should be reflected in any relevant policies.
  - Although this is only visible to people with API keys, API keys themselves are not scoped from email creation/email history viewing and we should keep this in mind when managing API keys.
