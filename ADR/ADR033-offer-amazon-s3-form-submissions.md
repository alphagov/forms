# ADR033: Offer Amazon S3 as an option to send form submissions

Date: 2024-06-04

## Status

Proposed

## Context

Users of GOV.UK Forms have asked for an alternative to email delivery of form submissions to allow integration with form processing systems.

Initially it was thought this might be acheived via POST to an http endpoint.

## Decision

Allow organisations to choose to send form submissions to an [Amazon S3](https://aws.amazon.com/s3/) bucket they host, with a policy configured to allow GOV.UK Forms to write to it. They can then integrate with their form processing systems as required.

```mermaid
---
title: Form submission to Amazon S3
---

graph LR

    classDef default fill:#fff,stroke:#333,stroke-width:2px;
    classDef forms fill:#000,stroke:#333,stroke-width:5px,color:#fff,font-size:28px;
    classDef org fill:#fe6,stroke:#fc3,stroke-width:5px,color:#000,padding:10px,font-size:20px;

    forms[GOV.UK Forms]

    class forms forms
    class gds gds

    subgraph org [Organisation]
        s3[\Amazon S3/]
        policy[/"bucket policy"/]
        processing{{Form Processing}}

        s3 ==> processing
        s3 --- policy
    end
    
    class org org

    data[/"structured<br/>data"/]
    file[/"optional<br/>file(s)"/]

    forms --> data --> s3
    forms -.-> file -.-> s3

```

## Consequences

* The receiving organisation must be using Amazon Web Services for this option to be suitable. An additional option may be required for organisations that can't use Amazon S3.
* When GOV.UK Forms supports file upload, these files can also be sent via Amazon S3
