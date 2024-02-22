# ADR027: Scheduled Smoke Tests

Date: 2024-02-22

## Status

Accepted

## Context

We want to run scheduled smoke tests that check critical user journeys like a
user completing and submitting a form. If a smoke test fails then the team
should be alerted through various channels depending on the required response
(e.g. Slack or Pager Duty out of hours).

## Decision

1. Use Ruby and Capybara to write the test code to maintain consistency with
   the end-to-end and application code already in use.
2. Use AWS CodeBuild to run the tests from an image containing the smoke test
   code along with Chrome and ChromeDriver; this is consistent with how the
   end-to-end tests are run in our pipelines during deployment. AWS Synthetic
   Canaries do not support Ruby at this time.
3. Schedule the running of the CodeBuild project with an AWS Event Bridge
   scheduled rule.
4. Use AWS CloudWatch Metric Alarm to alarm when a smoke test fails or when
   they stop running. The alarm will send to an appropriate SNS topic sending
   to either Slack or PagerDuty as required.
5. The smoke test infrastructure will exist in the same AWS account as the
   environment it is testing. This aligns with the strategy of self-contained
   accounts and environments.

## Consequences

1. Using Ruby and Capybara aligns with the existing team technology choices.
2. The tests run on infrastructure provisioned by AWS. This should improve
   reliability and reduce the maintenance burden over running on team
   maintained virtual machines.
3. Alerting remains consistent with existing solutions and can be modified to
   alert the appropriate channel from Slack to PagerDuty.
4. Engineers will need to access the production AWS account to begin debugging
   smoke test failures in production however this access would be necessary to
   debug the underlying cause anyway.
