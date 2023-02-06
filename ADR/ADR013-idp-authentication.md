# ADR013: Use another Identity Provider for authentication

Date: 2023-02-06

## Status

Proposed

## Context

In [ADR003 Use GOV.UK Signon](ADR003-use-govuk-signon.md) we recognised that

> We don't yet know if/how self-service account creation could work

Self-service account creation is essential to allow adoption to scale in public beta. This is not going to be possible with GOV.UK Signon so we need to find an alternative way to authenticate our users.

## Decision

We will evaluate different [Identity Providers](https://en.wikipedia.org/wiki/Identity_provider) and select one to use instead of GOV.UK Signon.

## Consequences

GOV.UK Forms will need to support multiple identity providers simultaneously so that Signon can continue to be used whilst we evaluate alternatives.

Authorisation now needs to be implemented directly in GOV.UK Forms. Currently Signon is used to authorise access to Forms and to determine which organisation a user belongs to.
