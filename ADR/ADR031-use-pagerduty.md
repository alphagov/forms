# ADR031: Use PagerDuty

Date: 2024-05-22

## Status

> Accepted or Rejected
>
> Valid ADR statuses are: "Proposed", "Accepted", "Rejected", "Deprecated", "Superseded by ADRzzz", but since we use the GitHub Pull request mechanism to approve ADRs, "Proposed" isn't applicable.

## Context

As GOV.UK Forms goes into public beta, we plan to begin out-of-hours support for the service. To do this, we need to be
able to have a number of things:

* a rota for who is responsible for out-of-hours support on any given day
* a way to notify the support person that something requires their attention
* a way to escalate to a second layer of support if the first person does not answer

These are not features we want to build for ourselves, so we must find a product which meets these needs.

## Decision

We have decided pay for the [PagerDuty](https://www.pagerduty.com/) service. This is the conventional approach within GDS, 
however that fact is not documented anywhere currently.

## Consequences
We are reliant on PagerDuty being operational to alert us to failures in our own service. The beneficial trade-off we 
get for this is a managed rotas and phone alerts system.