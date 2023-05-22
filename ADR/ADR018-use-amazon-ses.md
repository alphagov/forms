# ADR018: Use Amazon SES

Date: 2023-03-27

## Status

Accepted

## Context

### Attachments

In [ADR002 Use GOV.UK Notify](ADR002-use-govuk-notify.md) we recognised that

> GOV.UK Notify does not support email attachments

although it does have a way to [send files by email](https://www.notifications.service.gov.uk/using-notify/send-files-by-email) using download links. [User research](../research/2022-12-08_File_Upload_And_Optional_Questions_Processing.md) shows that

> Form processors preferred documents sent to them as attachments, not as individual links.

> Generally, people said the link version would take too long. 
> 
> Even small amounts of time can add up over many forms and efficiency is important.

### Formatting

[GOV.UK Notify message formatting](https://www.notifications.service.gov.uk/using-notify/formatting) is deliberately limited as it is designed to make emails sent to members of the public as simple as possible, which was the initial intention of Notify. Whilst it can and has been used to send messages to civil servants this is not an actively supported use case. This restricts what we can send to form processing teams who are more familiar with dealing with more complex emails.

GOV.UK Forms' first live incident was due to unexpected (undocumented) formatting behaviour that required [answers to be escaped](https://github.com/alphagov/forms-runner/pull/155).

### Security

Because it is intended to send emails to members of the public, GOV.UK Notify uses opportunistic TLS. There is currently no way to enforce TLS, or for clients to audit when TLS has been used. Whilst the risk is low due [guidance on securing government email](https://www.gov.uk/guidance/securing-government-email#encrypt-and-authenticate-email-in-transit), we cannot guarantee that any given message has been sent via TLS.

There isn't currently a way to audit which [GOV.UK Notify API keys](https://docs.notifications.service.gov.uk/rest-api.html#api-keys) have been used, and what for. This limits protective monitoring.

### Implementation

Amazon Simple Email Service (SES) addresses the Attachments, Formatting and Security issues outlined above.

GOV.UK Forms is in the process of being migrated onto AWS, so using Amazon SES is the obvious choice.

GOV.UK Notify uses Amazon SES to send emails, so there is already knowledge and experience within GDS on how to integrate with it.

## Decision

Use [Amazon SES](https://aws.amazon.com/ses/) directly instead of GOV.UK Notify for sending emails to form processing teams.

## Consequences

* emails sent to processing teams will go via Amazon SES. This includes:
    1. verification emails to confirm the correct email address
    2. submitted forms
* A `from` email address needs to be chosen and DNS needs to be configured securely
* An email template will need to be created
* GOV.UK Forms doesn't yet send email confirmations to members of the public who have completed forms. If / when this functionality is added, we need to decide if GOV.UK Notify is the most appropriate option.
