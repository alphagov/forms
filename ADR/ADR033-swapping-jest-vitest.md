# ADR032: Swapping JS Test Framework Jest for Vitest

Date: 2024-06-17

## Status

> Accepted

## Context

Jest tests are compatible with Vitest, but rather than running in a separate pipeline this allows us to consolidate into one run. It also means we have one less moving part to maintain.

This is a retroactive record of this [PR](https://github.com/alphagov/forms-admin/pull/1209).

## Decision

Adopt Vitest for our JS testing framework.

## Consequences

One less pipeline and addition to our Javascript build. Everything is Vite based.
