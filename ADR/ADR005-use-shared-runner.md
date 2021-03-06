# ADR005: Use shared runner

Date: 2022-04-07

## Status

Accepted

## Context

The forms platform has a "runner", the service that runs the forms itself to the user who is filling them in.

There are two different ways to approach the runner - a shared runner or a single runner per form. Two existing forms creation services (MOJ Forms, XGovFormBuilder) both use the single tenant approach.

### Runner per form

```mermaid
flowchart TD
  Manager[Form Manager]
  A[Form A]
  B[Form B]
  C[Form C]
  D[Form D]

  subgraph RunnerA[Runner]
    A
  end

  subgraph RunnerB[Runner]
    B
  end

  subgraph RunnerC[Runner]
    C
  end

  subgraph RunnerD[Runner]
    D
  end

  Manager --> RunnerA
  Manager --> RunnerB
  Manager --> RunnerC
  Manager --> RunnerD
```

In this structure, each form has its own runner which serves each form to the end user. This:

- Limits the impact if one form runner encounters an error
- Makes it more complicated to roll out updates to each runner as we scale
- Requires us to run a server consistently for all forms regardless of traffic, using up money + energy when not required

### Shared runner

```mermaid
flowchart LR
  Manager[FormManager]
  subgraph Runner
    A[Form A]
    B[Form B]
    C[Form C]
    D[Form D]
  end
  Manager --> Runner
```

In this structure, there is one runner service that serves forms to the end user. This:

- Enables us to have easier control over updating the runner where required (dependency version increases, service updates, etc.)
- Enables the ability to scale to the overall load on the forms service, removing the need to run idle servers for forms that have no traffic
- Increases the risk of a problem with one form affecting the performance of others

## Decision

We have decided to use a shared runner to host and run multiple forms.

## Consequences

We will be able to deploy updates to the runner more easily.

We will be able to scale the service to the total number of people filling in forms, rather than having idle servers for every low use form, reducing energy usage.

If the runner service encounters an error, all forms will be impacted rather than just one.
