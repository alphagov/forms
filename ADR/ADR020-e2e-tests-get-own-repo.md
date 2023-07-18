# ADR020: Move the e2e tests into their own repo

Date: 2023-07-14

## Status

Accepted

## Context

We have a set of end to end tests which are currently located in the `forms-deploy` repo [here](https://github.com/alphagov/forms-deploy/tree/main/capybara).

With the constant attention that the tests require, and the expansion of their coverage, it could be beneficial to separate them into their own github repository. This will make updating them; running them; and referring to them easier. 

### Naming

Based on other `alphagov` e2e repos, we could go with something like ***`forms-e2e-tests`*** for the repo name. This leaves plenty of room for other test formats i.e. `forms-smoke-tests`.

## Decision

We've decided to create a new repo for the e2e testsg

## Consequences

 - We have to (/get to) keep track of a new repo
 - Tests can be updated without requiring the `forms-deploy` repo to be in order
 - Test repo can have clearer dependencies and environment management
 - End to end tests can be public (forms-deploy repo is private)
