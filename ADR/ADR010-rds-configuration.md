# ADR010: Use of RDS Aurora Serverless V1 with Postgres

Date: 2022-11-17

## Status

Accepted

## Context

GOV.UK Forms requires postgres databases to store data. As part of re-platforming from GOV.UK PaaS to AWS these databases need to be provided by an AWS Service. AWS provide the Relational Database Service (RDS) which can be configured in various modes.

## Decision

Use RDS configured as Aurora Serverless V1 cluster with a postgres V11.13 engine. The main reasons for choosing this option are:
- Aurora Serverless V1 is compatible with the AWS Data API which provides IAM Authenticated means to query the databases via the AWS console or cli. This provides engineers with access for support, development debugging or incident response without needing to otherwise run a bastion within the VPC to reach the private RDS instances. Aurora Serverless V2 is not compatible with AWS Data API but is likely to be so later in 2023 according to our AWS Technical Account Manager.
- Aurora Serverless V1 can be configured to scale compute to zero when not in use and scale up under higher demand.
- Aurora Serverless was used in the Covid Response application and the lead developers concluded it worked well, especially praising the benefit of the AWS Data API integration.

## Consequences

- No bastion is required for ad-hoc database access. This reduces the maintenance and auditing normally associated for such a component.
- GOV.UK Forms downgrades from Postgres v13 as currently used on GOV.UK PaaS to Postgres v11.13 which is the latest offered by AWS Aurora Serverless V1. GOV.UK Forms is not currently reliant on [features exclusive to Postgres V13](https://www.postgresql.org/about/featurematrix/). GOV.UK Forms are considering a major change to the data model which could place greater reliance on JSON support. Postgres v11 does not support [JSON path expressions](https://www.postgresql.org/docs/current/functions-json.html#FUNCTIONS-SQLJSON-PATH). If this becomes a requirement then a migration to a more recent version of Postgres or alternative data storage solution may be necessary sooner.
- Aurora Serverless V1 will not gain support for more recent versions of Postgres according to our AWS Technical Account Manager. GOV.UK Forms will need to migrate from Aurora Serverless V1 as [Postgres v11 reaches end-of-life in November 2023](https://www.postgresql.org/support/versioning/). This is expected to happen once Aurora Serverless V2 gains support for AWS Data API and more recent version of Postgres. AWS provide [instructions for this upgrade in their documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.upgrade.html).
