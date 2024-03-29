# ADR003: Use GOV.UK Signon

Date: 2022-04-07

## Status

Superseded by [ADR015: Use an Identity Provider for authentication and implement authorisation](ADR015-idp-authentication.md).

## Context

GOV.UK Forms needs a way of authenticating users who will create and manage forms.

It would be preferable to make use of an existing authentication system rather than create a new one. We created 2 prototypes to better understand the effort to onboard and the account creation process.

## Decision

Use GOV.UK Signon to authenticate user access to GOV.UK Forms for form creation and management.

## Consequences

We don't have to build a new authentication system, and can start using the GOV.UK Signon Integration environment straight away.

We still need to decide if/how to use GOV.UK Signon Permissions for authorisation.

We still need to understand the process for creating accounts in private beta.

We don't yet know if/how self-service account creation could work.
