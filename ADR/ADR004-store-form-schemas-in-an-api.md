# ADR004: Store form schemas in an API

Date: 2022-02-18

## Status

Proposed

## Context

- Manager/Designer components don't need to be as scalable as the runner
- Runner needs to scale to number of users
  - Sustainability, runner not needed during quiet times
- "Published forms" need to be accessible to the runner

### Option 1 - Forms API

```mermaid
graph TD
  Manager[Form manager]

  subgraph formsApiService[Forms API]
    formsApi[API]
    formStore[(Form datastore)]
  end

  runnerRenderer[Forms renderer]
  Manager --> formsApi
  formsApi --> formStore
  formStore --> formsApi
  runnerRenderer --> formsApi
```

- Stores the forms in a datastore with the API being a separate application
- Runner depends on API
- Three applications to deploy with dependencies, too complex?
- Could cache API responses for speed

### Option 2a - Runner as an API

```mermaid
flowchart
  subgraph Manager
    managerService[Form manager]
    managerDatastore[(Form datastore)]
  end

  subgraph Runner[Runner application]
    api[Publish API]
    renderer[Forms renderer]
    store[(Published form datastore)]
  end

  managerService --> api
  renderer --> store
  managerService --> managerDatastore
  api --> store
```

- Stores the published forms alongside the runner
- Runner doesn't depend on api but exposes it instead
- Only two applications to deploy

### Option 2b - Publishing API, stores in shared datastore

```mermaid
flowchart
  subgraph Manager
    managerService[Form manager]
    managerDatastore[(Form datastore)]
  end

  subgraph SharedSpace[Shared space]
    subgraph Runner[Runner application]
      renderer[Forms renderer]
    end

    subgraph Publisher[Publishing application]
      api[Publish API]
    end
    store[(Published form datastore)]
  end

  managerService --> api
  renderer --> store
  managerService --> managerDatastore
  api --> store
```

- Stores the published forms in a datastore directly accessible to the runner
  - This doesn't necessarily have to be a database (e.g. S3 with a cache)
- Runner can be focused only on rendering
- Publish API separate
- Only two applications to deploy

### Option 3 - Manager and Runner share database

```mermaid
flowchart
  subgraph sharedSpace[GOV.UK Forms]
    subgraph manager[Manager application]
      managerService[Form manager]
    end

    formDatastore[(Form datastore)]

    subgraph runner[Runner application]
      formRenderer[Form renderer]
    end
  end

  managerService <--> formDatastore
  formDatastore --> formRenderer
```

- Form manager and runner share the same DB
- No need to build/maintain APIs
- Shared DB schema is a concern

### Option 4 - Monolithic manager and runner

```mermaid
flowchart
  subgraph sharedSpace[GOV.UK Forms]
    subgraph service[GOV.UK Forms application]
      managerService[Form manager]
      formRenderer[Form renderer]
    end

    formDatastore[(Form datastore)]
  end

  managerService <--> formDatastore
  formDatastore --> formRenderer
```

- Single application to deploy
- Single DB schema to maintain
- Updates to manager will impact the runner

## Decision
## Consequences

> both positive and negative consequences of the decision
