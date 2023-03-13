# ADR014: Use an Identity Provider for authentication and implement authorisation

Date: 2023-02-06

## Status

Accepted

## Context

In [ADR003 Use GOV.UK Signon](ADR003-use-govuk-signon.md) we recognised that

> We don't yet know if/how self-service account creation could work

Self-service account management is essential to allow adoption to scale in public beta. This is not going to be possible with GOV.UK Signon so we need to find an alternative way to authenticate our users.

GOV.UK Signon requires an existing user with an Admin role to either create a new user or give an existing user permission to access GOV.UK Forms. We are looking to implement a self-service model similar to GOV.UK Notify and GOV.UK Pay where users can get initial access without needing an account to be created for them by someone else. User permissions are then managed by other users within the product itself.

## Decision

We will evaluate different [Identity Providers](https://en.wikipedia.org/wiki/Identity_provider) and select one to use instead of GOV.UK Signon.

## Consequences

GOV.UK Forms will need to support multiple identity providers simultaneously so that Signon can continue to be used whilst we evaluate alternatives.

Authorisation now needs to be implemented directly in GOV.UK Forms. Currently Signon is used to authorise access to Forms and to determine which organisation a user belongs to, so an equivalent concept of Admin roles in GOV.UK Signon needs to be implemented in GOV.UK Forms.
