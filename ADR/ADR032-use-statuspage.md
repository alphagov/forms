# ADR032: Use StatusPage

Date: 2024-05-22

## Status

> Accepted or Rejected
>
> Valid ADR statuses are: "Proposed", "Accepted", "Rejected", "Deprecated", "Superseded by ADRzzz", but since we use the GitHub Pull request mechanism to approve ADRs, "Proposed" isn't applicable.

## Context

As GOV.UK Forms goes in to public beta and beyond, we expect our user base to expand, and to be overall less directly 
engaged with our users. We have good means for broadcasting product news to our users, but we don't yet have a way of
broadcasting information about ongoing incidents. We will need that ability, and it should be external to the service
so that a service outage is not also on outage to our ability to communicate about said outage.

## Decision

We have decided to pay for the [StatusPage](https://www.atlassian.com/software/statuspage) service. This is the
conventional approach within GDS, however that fact is not documented anywhere currently.


## Consequences
We are reliant on StatusPage being operational to alert our users to ongoing incidents. The beneficial trade-off we
get for this is a managed and reliable service for reporting incidents.