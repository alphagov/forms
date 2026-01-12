# ADR048:Store form started and submitted counts in database

Date: 2026-01-12

## Status

Accepted

## Context

We provide form metrics to administrative users of the platform, available in the forms-admin application. This details
how many forms have been started and how many have been submitted per form. We allow users to download this data as a CSV
file.

Currently, we store these metrics in CloudWatch - which has a retention period of 455 days (15 months) at an hourly 
granularity.

The main disadvantages of this approach are:
- We are only able to provide metrics for the last 15 months. This means users need to remember to download and store the data if they need it over a longer period.
- Code changes to how we display metrics are difficult to test as we cannot easily set up test data in CloudWatch.
- Internally, we use a mix of manual processes and the Splunk logs which we know historically have not received all log events for our performance analytics.

## Decision

Store the form started and submitted counts in the PostgreSQL database used by forms-admin. We will add a new table 
to store daily counts of form starts and submissions per form.

Forms-runner will make API calls to forms-admin to increment the counts when a user starts or submits a form. Forms-runner
is already able to make API calls to forms-admin for retrieving form data, so no infrastructure changes are required to support this.

We will use the `ON CONFLICT DO UPDATE` feature of PostgreSQL to increment the counts atomically.

## Consequences

- We are able to store metrics indefinitely for Forms, allowing us to provide longer term metrics to users
- We will only store metrics with a daily granularity.
- We can more easily set up test data for testing changes manually and in automated tests
- We can more easily create reports for internal performance analysis