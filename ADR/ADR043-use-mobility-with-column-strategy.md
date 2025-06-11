# ADR043: Use Mobility gem with :column strategy to manage translated fields

Date: 2025-06-09

## Status

Accepted

## Context

We plan to add support for bilingual English and Welsh forms to the platform. To do this, we need a way of storing the user-created text (such as form names, question text, and guidance) for each language.

English and Welsh are the only languages we plan to support at the moment, but we are aware that we may need to support more languages at some point in the future.

### Storage strategies

The main strategies for storing translations are:

- Translatable columns
  - adding new columns for each translatable column to the existing model table for each new language
- Model translation tables
  - adding a new table for each existing model to hold translations
- Shared translation tables
  - adding a new table which will hold translations for all models
- Serialized data
  - storing translations in an existing column as a JSON string or another serialized format
- PostgreSQL jsonb
  - essentially a variant of the serialized data strategy that takes advantage of PostgreSQL's jsonb column type to make data easier to query.

#### Translatable columns
Advantages:
- Simple to understand and work with
- Easy to query

Disadvantages:
- Since new columns need to be added to every table for every language, the maintenance burden increases as the number of locales increases
- Since every new model would require new columns, maintenance burden increases as number of models increases
- Inefficient use of database space

We currently have a small number of models and locales which mitigates the main disadvantages, so this seems like a good option for us.

#### Model translation tables
Advantages:
- Scales well with locales (since all locales can use the same table)
- Uses space more efficiently than translatable columns

Disadvantages:
- Adds one extra table per model, so maintenance burden increases as the number of models increases
- Requires table joins, creating increased complexity and risk of performance issues

This could be a good option for us, since we have a small number of models.

#### Shared translation tables
Advantages
- Versatile, no additional migrations required when adding new locales or models

Disadvantages
- Requires more complex table joins, creating increased complexity and risk of performance issues
- since tables don't map 1:1 with model tables, it's harder to keep the shared table up to date with attribute renames and dropped columns

This could work for for us, but might be needlessly complex for the number of models and locales we're currently expecting to have.

#### Serialized data
Advantages:
- Simple to understand and work with

Disavantages:
- Difficult to add constraints
- Difficult to query

We recommend against this option - the PostgreSQl jsonb strategy is functionally similar with fewer disadvantages. 

#### PostgreSQL jsonb
Advantages:
- Simple to understand and work with

Disavantages:
- Difficult to add constraints

We think the inability to easily add database constraints makes this a poor option for our use case.

### Gems
There are a few popular Ruby gems for dealing with translations. We looked into:

- [Mobility](https://github.com/shioyama/mobility)
- [Globalize](https://github.com/globalize/globalize)
- [Traco](https://github.com/barsoom/traco)
- [Puret](https://github.com/jo/puret)

Of these, only Mobility and Globalize have received recent updates. Mobility is actively maintained. Globalize is still maintained, but the maintainers recommend Mobility for new projects.

Mobility also supports all of the backend strategies we've looked at, with largely the same API for each, which means it would be helpful if we decided we wanted to change strategy later.

We also considered the possibility of implementing our own solution without using a gem. In this case we’d:
- Have one less dependency
- Have more control over our implementation
- Have to manage database changes manually
- Have to manage the translation retrieval manually (which could get cumbersome if we add more locales or models, and especially cumbersome if we try to use the model or shared translation tables strategies)
- Have to do more work if we decide to change strategy

## Decision

We have decided to:
- implement translatable columns for each translatable text field
- use the Mobility gem, configured with the `:column` backend strategy, to manage this

## Consequences

- when adding new models, we will need to add columns for translatable fields
- if we add new languages we will need to add additional columns for each translatable field
- when adding new models or languages, we should assess whether we've outgrown the translatable columns strategy
- if we decide to change storage strategy, using Mobility should minimise the number of app changes required
