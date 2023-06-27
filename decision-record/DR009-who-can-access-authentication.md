# DR009: Deciding who can access GOV.UK Forms

Date: 2023-06-27

## Status

> Proposed

## Context

> While looking at replacing Signon with either CDDO's SSO, or Auth0, it was raised that restricting users to gov.uk email accounts only would still allow non-central government organisations, such as local councils, access to create an account.

We are currently restricting GOV.UK Forms to central government departments, so this was discussed as a risk of inadvertently expanding our scope.

## Decision

> it was decided that this was not an issue - users from local government will only be able to make an account with trial permission. Anything further would require a Super Admin (ie. the GOV.UK Forms team) to set up an organisation for them, and set up admins for that org. Therefore, we still have control over access to just central government for now.

## Consequences

> It means when we do eventually expand to allow other public sector organisations like local councils, we don't need to do too much extra work to allow this. However, we need to manage expectations before users sign up, so they're aware who will have access, or what access they'll have if they're not from a central government department.
