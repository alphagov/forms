# GOV.UK Forms Sequence Diagrams 

## Introduction

The diagrams in this folder (created using [Mermaid](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams#creating-mermaid-diagrams)) show the interactions between users and GOV.UK Forms, including the two main applications [forms-admin](https://github.com/alphagov/forms-admin) and [forms-runner](https://github.com/alphagov/forms-runner).

The diagram below is to provide an overview of the different users and systems that interact with each other. For clarity, not all interactions are shown. Please refer to individual sequence diagrams for detailed interactions.

## High Level Architecture of GOV.UK Forms

```mermaid
graph TD
    subgraph users
        super_admin((GOV.UK Forms<br/>Team<br/><br/>Super Admin))
        editor((form editor))
        content((content designer))
        filler((Person filling in a form))
        processor((form processor))
    end

    auth0(Auth0)
    sso(Google Workspace)
    govuk(GOV.UK website)

    super_admin --- sso --- auth0
    editor --- auth0
    content --- govuk

    subgraph sg1 [GOV.UK Forms]
        admin(forms-admin)
        runner(forms-runner)
    end

    editor---runner

    auth0 --- admin
    filler --- govuk
    filler --- runner --- admin

    notify(GOV.UK Notify)
    ses(Amazon Simple Email Service)

    pay(GOV.UK Pay)
    filler -.- pay -.- runner

    filler -.- notify
    notify -.- runner
    ses --- runner
    processor --- ses
```

## Links to Sequence Diagrams

* [authentication](authentication.md)
* [creating a form](creating-a-form.md)
* [publishing a form](publishing-a-form.md)
* [filling in a form](filling-in-a-form.md)
* [changing a form](changing-a-form.md)

