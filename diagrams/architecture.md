# Architecture Diagram

This diagram represents our most up to date view of the GOV.UK Forms architecture.

Each box doesn't necessarily correspond to a different application running, but instead "components" that form part of the entire GOV.UK Forms platform (E.g. The designer/manager could be the same application, but are distinct components to talk about).

```mermaid
graph
  proposed[Proposed component]
  proposedLater[Proposed for later in private beta]
  existing(Existing system)

  classDef futureComponent stroke-dasharray:3;
  class proposedLater futureComponent
```

```mermaid
flowchart
  classDef subgraphPadding fill:none,stroke:none
  classDef futureComponent stroke-dasharray:3;

  subgraph github[Github]
    alphagov/forms
  end

  subgraph monitoring[Monitoring services]
    logit(Logit)
    splunk(Splunk)
    sentry(Sentry)
  end

  subgraph paas[GOV.UK PaaS]
    subgraph paasPadding[ ]
      subgraph paasForms[GOV.UK Forms]
        subgraph paasFormsPadding[ ]
          subgraph internal["Internal Users (Government Departments)"]
            authorisation[Authorisation]
            authentication[Authentication]
            manager[Forms manager]
            designer[Forms designer]
            api[Forms persistence API]
            formDb[(Form data)]
            userDb[(User data)]

            manager --> api
            designer --> api
            api --> formDb
            manager --> userDb
            authorisation --> manager
            authorisation --> designer
            authentication --> manager
            authentication --> designer
          end
          
          subgraph external["External Users (Members of the public)"]
            runner[Form runner]
            submitter[Form submitter]
            userSessions[(User session data)]
            fileUpload[Form file upload]

            runner --> userSessions
            runner --> submitter
            class fileUpload futureComponent
          end

          events[Events collector]
          api --> runner
        end
      end
    end
  end

  subgraph dependencies[External dependencies]
    pay(GOV.UK Pay)
    places(OS Places API)
    signin(GOV.UK Sign In)
  end

  notify(GOV.UK Notify)
  formUser{{Form user}}
  formProcessor{{Form processor}}
  adapter(Adapter)
  existingApi(Existing API)

  submitter --> notify
  notify --> formUser
  notify --> formProcessor
  submitter --> adapter
  adapter --> existingApi
  runner -.-> dependencies

  github --"CI/CD"--> paasForms
  paasForms --> monitoring

  class paasPadding subgraphPadding
  class paasFormsPadding subgraphPadding
  class adapter futureComponent
```
