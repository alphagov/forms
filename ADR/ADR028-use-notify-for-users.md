# ADR029: Use GOV.UK Notify for emails sent to users for simple notifications

Date: 2024-03-28

## Status

Accepted


## Context

This is an addendum to [ADR019](ADR019-use-amazon-ses.md) which set out the intention to use Amazon's Simple Email Service instead of GOV.UK Notify to send emails.

GOV.UK Forms has continued to use GOV.UK Notify to send emails including:
- submission confirmation emails to members of the public who have completed a form.
- the submitted forms to the service processing them.
- One Time Passcodes to verify the ownership of the submission email address when creating or editing a form.

Amazon SES is currently used during the authentication process when logging into the form builder via Auth0, a third party authentication service, to send One Time Passcodes since Auth0 does not offer integration with the GOV.UK Notify API. Using Amazon SES also provides enforced TLS.

GOV.UK Forms now needs to send notifications to users relating to account management (such as when they are upgraded from a trial to full user account).

## Decision

GOV.UK Forms will use GOV.UK Notify where the service is appropriate and does not require the additional features that Amazon SES offers.

## Consequences

- GOV.UK Forms does not need to invest in building additional monitoring, alert and administrative interfaces related to sending email which GOV.UK Notify already provide.
- GOV.UK Forms will be dependent upon the support, reliability and feature roadmap of GOV.UK Notify, for example if and when they offer enforced TLS to the recipients inbox.
