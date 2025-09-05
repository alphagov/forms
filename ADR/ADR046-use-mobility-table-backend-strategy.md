# ADR046: Use Mobility's table backend strategy to store translations

Date: 2025-09-08

## Status

Accepted

## Context

We previously decided in [ADR043: Use Mobility gem with :column strategy to manage translated fields](ADR043-use-mobility-with-column-strategy.md) that we would use Mobility's column strategy to handle storing translations.

Our initial proposal was to use the column strategy (the simplest strategy Mobility supports) while we had a small number of languages (English and Welsh), and reassess later whether to use a more elaborate strategy if we add more languages. We concluded that Mobility's table strategy (described as 'Model translation tables' in the earlier ADR) scales better with an increased number of languages, so this is likely to be a better option than the column strategy if we need to support more than a few languages.

In conversations with departments we have found that there is demand for supporting additional languages, so we think we are likely to need the more scalable backend strategy.

Rather than implement the column strategy initially and migrate to the table strategy later, it would be less work to implement the table strategy directly.

## Decision

We have decided to:

- implement translation tables for each model
- use the Mobility gem, configured with the `:table` backend strategy, to manage this

## Consequences

- adding additional languages in future should be easier
- when adding new models, we will need to add a translation table for each new model
