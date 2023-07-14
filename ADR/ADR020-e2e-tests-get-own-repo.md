# ADR020: Move the e2e tests into their own repo

Date: 2023-07-14

## Status

Proposed

## Context

We have a set of end to end tests which are currently located in the `forms-deploy` repo [here](https://github.com/alphagov/forms-deploy/tree/main/capybara).

With the constant attention that the tests require, and the expansion of their coverage, it could be beneficial to separate them into their own github repository. This will make updating them; running them; and referring to them easier. 

## Decision

> what the team has decided to do

## Consequences

 - We have to (/get to) keep track of a new repo
 - Tests can be updated without requiring the `forms-deploy` repo to be in order
 - Test repo can have clearer dependencies and environment management


> both positive and negative consequences of the decision
