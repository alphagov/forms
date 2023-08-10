# ADR021: Use Auth0 as an Identity Provider for Authentication

Date: 2023-08-09

## Status

Accepted

## Context

Following [ADR015: Use an Identity Provider for authentication and implement authorisation](ADR015-idp-authentication.md) we looked into alternatives to GOV.UK Signon.

[NCSC guidance on Enterprise authentication policy](https://www.ncsc.gov.uk/collection/device-security-guidance/infrastructure/enterprise-authentication-policy) states:

> Where possible, reduce reliance on passwords and implement passwordless authentication

and there is [NCSC guidance on one time passwords](https://www.ncsc.gov.uk/guidance/authentication-methods-choosing-the-right-type#section_5).

[UK Government Security Single Sign-On](https://sso.service.security.gov.uk/) was considered, but is still in an "Alpha" phase.

[Auth0 offers Passwordless Authentication Methods](https://auth0.com/docs/authenticate/passwordless/authentication-methods) so was also considered, and a DPIA (Data Protection Impact Assessment) was carried out.

[User research on authentication](../research/2023-08-Usability_Testing_Authentication.md) showed that participants were comfortable using a passwordless process and preferred the Auth0 journey.

## Decision

We will use [Auth0 passwordless authentication with email](https://auth0.com/docs/authenticate/passwordless#email) to authenticate users who access GOV.UK Forms.

(Note that this is only for users creating and managing forms. Users who fill in forms are currently unauthenticated.)

## Consequences

We make use of the [Auth0 OmniAuth Strategy gem](https://github.com/auth0/omniauth-auth0).

We need to [configure Auth0 to use Amazon SES as an external SMTP email provider](https://auth0.com/docs/customize/email/smtp-email-providers/configure-amazon-ses-as-external-smtp-email-provider) (we decided to use SES as part of [ADR019: Use Amazon SES](ADR019-use-amazon-ses.md)).

The Auth0 DPIA needs to be reviewed and updated when GOV.UK Forms moves into Public Beta phase and beyond.

An Enterprise Subscription may be required in the future, e.g. for SLA and support, or to use advanced features.

We can decide to use a different OIDC-compatible identity provider in the future, e.g. to align with other government systems.