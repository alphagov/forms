# ADR039: Add another Aurora cluster to provide database to Forms Runner

Date: 2025-01-27

## Status

Accepted

## Context

To support using SolidQueue (see [ADR38](ADR038-add-psql-database-and-solid-queue-to-forms-runner.md)) and for supporting storing of user's answers before they complete a submission (Save and Return) we will need a database. However we don't want to store alongside the data for forms. One reason being is if we need to recover, that affects both the submissions data and the data on forms themselves, leading to potential loss of data on both sides. We will provision a separate Aurora cluster for a stronger partition of data. The pre-submission data is inherently transient anyway (once it's sent, we won't store it for long), whereas we cannot lose the definitions of forms, users (form creators), groups and orgs.

## Decision

We will provision another Aurora cluster and store data relating to submissions there, separate to the cluster where the databases for API and Admin live.

## Consequences

* We will need more infrastructure to support the Aurora cluster
* We will have 2 clusters to maintain
* Runner will store and read data separate to the API and Admin apps
