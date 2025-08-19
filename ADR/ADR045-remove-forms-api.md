# ADR045: Remove forms-api

Date: 2025-08-19

## Status

Accepted

## Context

In [ADR004: Store form schemas in an API] we decided to implement a separate API app so that we could scale the services required for form submissions separately to the services required for building forms.

However, maintaining multiple apps has resulted in increased toil. Having multiple services has also resulted in challenges around designing and maintaining the interface between forms-admin and forms-api.

As the cost of compute is low at the moment, the cost of the additional developer time outweighs any savings due to efficient capacity management.

We are currently refactoring forms-admin and forms-api to work with the v2 API described in [ADR034: API v2 for Forms]. We have an opportunity now as part of this work to make a large architectural change, namely using the forms-admin app to serve the v2 API endpoints needed for forms-runner, and removing the need for forms-api.

[ADR004: Store form schemas in an API]: ADR004-store-form-schemas-in-an-api.md
[ADR034: API v2 for Forms]: ADR034-api-v2-for-forms.md

## Decision

We will add endpoints to forms-admin that can be used to retrieve v2 API form documents in JSON format.

We will change forms-runner to read form documents from these new endpoints in forms-admin.

We will keep the new endpoints in forms-admin accessible from the private VPC only (keep them not accessible from the public internet), and not require authentication for their use.

We will retire the forms-api app and remove it, its database, and associated systems, networks and configuration files.

The plan to follow to achieve this is documented separately, in [Migrating forms-admin to v2 API (Google Docs)](https://docs.google.com/document/d/1Ea2rEK3gcaRhAVKiLIelD8FNxNI7YHqWmKSfbzMjeLQ/).

## Consequences

Positives:
- We will have fewer separate apps to maintain

  For each app we have to maintain we have additional maintenance workload,
  including regular security patches, keeping files common to all repositories
  in sync, and other causes of toil. Fewer apps means less toil for developers.

Negatives:
- forms-admin will be in the critical path for submitting a form

  The system will be less resilient (all other things being equal) because an
  issue in forms-admin could cause form submissions to fail. We could look at
  ways to mitigate this loss of resilience if it is thought to be necessary.

- We won't have an external API for retrieving form documents

  This will make it harder for developers to debug and/or investigate the
  production system, but we have found that with the current API it is not
  common for developers to make API requests directly to forms-api. If we find
  that there is a need we can consider adding an external API with access
  control.

### Consequences for costs and resource usage

This change is likely to be resource-neutral, in the best case it may use
slightly less resources, but it is more likely it will increase our resource
usage. Currently we have fewer forms-admin instances than forms-api instances
running in production, but each forms-api instance uses more compute. It is
difficult to predict what the right number of instances for the forms-admin app
including API endpoints would be, we will probably over-provision initially and
optimise resource usage later.

In terms of costs we are currently on a [compute savings plan] that has pay a
fixed annual cost for a pre-agreed amount of compute, so we may not see an
increase of cost.

In terms of CO2 usage our AWS systems are currently nominally carbon-neutral,
as Amazon has "purchased renewable energy that compensated all or part of the
emissions associated with [our] usage", and the change in this ADR is unlikely
to increase our emissions beyond the point of being carbon-neutral.

If we do find that we need to improve the scaling properties of the system, we
could consider cache layers between forms-admin and forms-runner rather than a
full API.

[compute savings plan]: https://aws.amazon.com/savingsplans/compute-pricing/
