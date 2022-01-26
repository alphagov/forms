# ADR001: Implement continuous deployment

Date: 2022-01-26

## Status

Accepted

## Context

The GDS Way recommends that teams [use continuous delivery](https://gds-way.cloudapps.digital/standards/continuous-delivery.html#use-continuous-delivery). 

All of our code is currently stored in Github, and our team already has a GOV.UK PaaS account.

## Decision

We will use Github Actions to run our workflows. When we create a new repository, we should set up a deployment workflow which will run after commits on the main branch.

We will use GOV.UK PaaS for our environments where this is possible.

## Consequences

We expect this to reduce the time between iterations and allow us to get more frequent feedback on our changes.

We will be able to add automated tests where apppropriate to validate our changes.
