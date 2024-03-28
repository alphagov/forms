# ADR029: Use GOV.UK Notify for emails sent to users for simple notifications

Date: 2024-03-28

## Status

Accepted


## Context

Emails to users that confirm they have submitted their form, and as notifications for their user account management (such as when they are upgraded from a trial to full user account, need to be sent. We currently only use Amazon SES for submission emails where TLS requirements are higher. This is an addendum to [ADR019](ADR019-user-amazon-ses.md).

## Decision

We will use GOV.UK Notify where the service is appropriate and does not require the additional features that Amazon SES offers.

## Consequences

We keep using a free and simpler mechanism for sending emails to our users.
