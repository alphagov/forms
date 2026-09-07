# ADR052: Store analytics in S3 Tables and query with Athena, or in a separate Aurora database

Date: 2026-09-07

## Status

Proposed

This record sets out two options for team discussion rather than a single decision. Once a choice is made it will be recorded here and the status changed to Accepted.

## Context

We want to measure key performance indicators for GOV.UK Forms, starting with:

- the number of submissions over time
- the number of live and archived forms over time

We need at least 2 years of data for year-on-year comparisons. Longer retention is preferred provided it is cheap and efficient for us.

These are business analytics rather than operational monitoring. Accuracy matters. The data does not need to be real-time, but having up-to-date figures is useful.

forms-runner already logs a structured `form_submission` event for every submission.

Recording the number of submissions per form and the number of forms per organisation is not a necessity, but the granularity would be useful if we later wanted to reuse the metrics for form-level analytics.

### Options considered and rejected

**CloudWatch OpenTelemetry metrics (tried).** This is AWS's current, recommended metrics model, billed per GB ingested with 15 months of retention. Metrics are statistical aggregates, not a record of events, so should not be used for anything that needs exact figures. For example, counters are aggregated in-process and exported on an interval, so counts are lost if a task exits before export, and PromQL `rate()` and `increase()` extrapolate across the query window and can return non-integer results. The OpenTelemetry SDK also caps each metric at 2,000 attribute combinations by default, after which per-form measurements collapse into a single overflow bucket.

**CloudWatch Classic metrics.** Every unique dimension combination is a separately billed metric at $0.30 per metric per month, so a per-form dimension costs roughly $0.30 per form per environment per month and grows with every form we host. Metrics expire after 15 months.

**Google Analytics 4.** Client-side events only fire after a user accepts usage cookies, so they undercount. The server-side Measurement Protocol requires a user id on every event, so we would have to create pseudo ids. Sending submissions with fabricated ids either inflates user counts or lands them under "(not set)", polluting our real user metrics. A per-form dimension exceeds GA4's 500-value high-cardinality threshold, so less common forms are condensed into an "(other)" row. Event-level data is retained for at most 14 months on a standard property.

**Splunk.** We keep logs for 12 months, it is not a tool we own, and we intend to move away from it.

**CloudWatch Logs Insights over existing logs.** This needs no new infrastructure, but every query scans the whole runner log group rather than just submission events, so we pay for and wait on data we do not need. Keeping the whole log group for years to preserve a handful of events would be wasteful.

**The forms-runner database.** This would grant observability tooling access to a database with potentially sensitive information, and analytics queries could affect production performance.

**Amazon Redshift Serverless or OpenSearch.** Both are capable, but their cost far exceeds what a few small tables need.

## Decision

Two options are outlined below. The following applies to both:

- Only non-sensitive fields are stored: form identifiers and metadata, never answers or personal data.
- Isolated from production databases, so analytics queries cannot affect production performance.
- We can set our own retention limits.
- Both can be queried by data visualisation tools (each has a Grafana datasource).
- Data can be moved between either option if we need to change decision.

### Option A: Amazon S3 Tables, queried with Amazon Athena

Amazon S3 Tables is storage optimised for analytics workloads. Tables are stored in Apache Iceberg format and can be queried by any engine that supports Iceberg. Athena is a serverless query engine that supports Iceberg and S3 Tables.

Each environment gets an S3 table bucket with a `forms` namespace.

Initially, events are taken from the structured log lines the applications already emit: a CloudWatch Logs subscription filter selects them, a small Lambda transform maps them to the table schema, and Kinesis Data Firehose writes them to the table. This needs no application changes. Later, the applications could write events directly, removing the dependency on the log format. The decision here is primarily where the data lives and how it is queried.

Pros:

- Negligible cost, less than $10 per year per environment: the main costs are S3 storage and Athena's per-query charge.
- Fully managed. S3 Tables handles compaction and snapshot maintenance; Firehose, Lambda and Athena have no servers.
- S3 durability and availability.
- Fast to set up, already have working prototype, no application changes.

Cons:

- Unfamiliar services: S3 Tables, Firehose and Athena.
- Firehose delivery is at-least-once, so queries may need de-duplication or the transform needs an idempotency key.
- Table schemas are defined in Terraform, but the provider does not support partitioning yet (not a big concern at our scale).
- Athena queries take seconds, too slow for the request path. Showing per-form statistics in forms-admin would need a faster way to query.

### Option B: a separate Aurora PostgreSQL cluster for analytics

A new database, separate from the forms-admin and the runner databases, holding only analytics tables. The applications write events to it directly through a second Rails database connection.

Pros:

- Familiar. We already run Aurora PostgreSQL.
- Transactional, exactly-once writes with no log parsing.
- Indexed rows give low-latency queries, which suits serving per-form analytics inside forms-admin later.
- No new services to learn.

Cons:

- Always-on cost, about $500 per year per environment, as the cluster must run whenever we accept submissions.
- More to manage: engine upgrades, backups and credentials.
- A row store is not designed for analytical queries, although not a problem at our current scale.
- Durability depends on our own backup and restore.

## Consequences

If we choose Option A:

- Greater vendor lock-in with S3 Tables and Athena, although we have considerable lock-in already.
- Duplicate records are possible and must be handled.
- Cannot be used directly for product-facing analytics.

If we choose Option B:

- More expensive.
- Less performant once the dataset grows.

Either way:

- We also need to implement a way to visualise this data.
