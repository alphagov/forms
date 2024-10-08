# ADR035: Offer Amazon S3 as an option to send form submissions

Date: 2024-10-08

## Status

Accepted

## Context

Sending form submissions via email is useful for teams who already receive forms in an email inbox. Some users of GOV.UK Forms have asked for an alternative to email delivery of form submissions to allow automated integration with form processing systems.

Initially it was thought this might be acheived via a [webhook mechanism similar to GOV.UK Pay](https://docs.payments.service.gov.uk/webhooks/), which requires setting up a custom endpoint that is both available and secure, with the associated ongoing support and maintenance. Advice from NCSC encouraged us to explore the use of managed services as alternatives to a self-hosted webhook.

## Decision

Allow organisations to choose to send form submissions to an [Amazon S3](https://aws.amazon.com/s3/) bucket they host, with a policy configured to allow GOV.UK Forms IAM role to write to it. They can then integrate with their form processing systems as required.

```mermaid
---
title: Form submission to Amazon S3
---

graph LR

    classDef default fill:#fff,stroke:#333,stroke-width:2px;

    subgraph forms_aws [GOV.UK Forms AWS Account]
        forms[GOV.UK Forms]
        role[/"IAM role"/]

        role --- forms

    end

    subgraph org [Organisation AWS Account]
        s3[\Amazon S3/]
        policy[/"bucket policy<br />allows IAM role"/]
        event[/s3:ObjectCreated event/]
        processing{{Form Processing}}

        s3 --- event --- processing
        s3 --- processing
        s3 --- policy
    end
    

    data[/"structured<br/>data"/]
    file[/"optional<br/>file(s)"/]

    forms --> data --> s3
    forms -.-> file -.-> s3

```

## Consequences

* The format of the `structured data` that represents the submitted form can be defined in a separate ADR.
* The receiving organisation must be using Amazon Web Services for this option to be suitable. An additional option may be required for organisations that can't use AWS and/or Amazon S3.
* When GOV.UK Forms supports file upload, these files can also be sent via Amazon S3.
