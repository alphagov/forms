# ADR033: Offer Amazon S3 as an option to send form submissions

Date: 2024-06-04

## Status

Proposed

## Context

Users of GOV.UK Forms have asked for an alternative to email delivery of form submissions to allow integration with form processing systems.

On 4th December 2023 we held a "Defining GOV.UK Forms API integration" technical discussion with representation from several other government organisations.

## Decision

Allow organisations to choose to send form submissions to an [Amazon S3](https://aws.amazon.com/s3/) bucket they host.

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
        processing[Form Processing]
        s3[\Amazon S3/]

        s3 -.-> processing 
    end
    
    class org org

    data[/structured<br/>data/]

    forms --> data --> s3

```

## Consequences

> both positive and negative consequences of the decision
