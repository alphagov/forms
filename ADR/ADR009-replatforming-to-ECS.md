# ADR009: Re-platforming GOV.UK Forms to AWS ECS Fargate

Date: 2022-10-27

## Status

Accepted

## Context

GOV.UK Forms currently runs on GOV.UK PaaS which is being decommissioned in
December 2023 and all tenants must re-platform.

## Decision

Move GOV.UK Forms onto AWS Elastic Container Service (ECS) with Fargate and supporting
AWS services such as RDS and Elasticache. All infrastructure to be managed with
Terraform. Continuous integration and deployment patterns will be implemented
(technology choices are TBD).

## Consequences

- AWS ECS and supporting AWS services are well understood and used by a number
of other GDS products. We can make use of existing experience and expertise.
- The current and expected future infrastructure requirements of GOV.UK Forms can be met.
- Fargate deployment mode takes care of the underlying VM management to reduce
the maintenance burden.
- High level of confidence that GOV.UK Forms will work as-is with AWS services because they
are already being used by the GOV.UK PaaS implementation (e.g. RDS and
Elasticache).
- Feature development will continue throughout the migration with GOV.UK Forms
being dual deployed to PaaS and ECS until cut-over.
- The GOV.UK Forms team will need to manage more infrastructure since GOV.UK PaaS
will no longer be taking care of much of it.  This will require more engineering
time to be spent on building and maintaining infrastructure which will likely
require either up-skilling developers with Site Reliability Engineering (SRE)
skills or adding extra Site Reliability Engineers to the team.
- Some team members will need to learn more about working with AWS services directly.