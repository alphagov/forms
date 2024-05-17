# ADR030: Use AWS Lambda to run glue code

Date: 2024-05-17

## Status

> Accepted or Rejected
>
> Valid ADR statuses are: "Proposed", "Accepted", "Rejected", "Deprecated", "Superseded by ADRzzz", but since we use the GitHub Pull request mechanism to approve ADRs, "Proposed" isn't applicable.

## Context

There are, in this context, two types of code we want to consider

1. Application code
2. Glue code

Application code is written by the developers on the team, and makes up the GOV.UK Forms service and all of
its functionality. It is executed to handle HTTP requests received by a long-lived web server process, and it has access
to stateful data storage like PostgreSQL and Redis.

In contrast, glue code isn't part of any application, but is required to support the function of the service or its 
infrastructure in some way. Examples of that could include code for integrating two independent systems, or code for 
testing the state of something periodically.

This ADR addresses where we run infrastructure code, and provides guidance on when not to follow the ADR.

Our application code runs in containers on [AWS ECS on Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html).
It is a managed service which is well suited to running long-running processes like web servers. It has a somewhat involved
setup process and its use of containers incurs some maintenance and operational overhead, but that is a worthwhile
trade-off for its functionality and stability. It is also able to run short-lived tasks.

However, for infrastructure code, which is often characterized by being small, quick to run, and not requiring a connection to
any stateful data stores, the overhead of the different pipelines and configurations required to run in ECS becomes
disproportionate to the size of the code and the frequency with which we think about it. We can quickly end up with more
code for running and configuring the thing than code in the thing we want to run.

AWS Lambda is AWS' serverless functions-as-a-service service. It be given a source code bundle and it can execute the code within
based on a small amount of configuration. Its primary target use case is in running code in response to events, without the
need for a long running server. This matches up well with the types of use cases we have for glue code.

## Decision: use AWS Lambda to run glue code

We will use AWS Lambda for workloads that meet these criteria:
* aren't application code
* are glue code
* are short-lived
* are written in Ruby
* are infrequently run (including on a schedule)
* do not require access to persistent data storage
* run asynchronously in response to some event
* are not handling HTTP requests

## When should I not use AWS Lambda?

There are some glue code workloads that require access to persistent data stores, for example a daily job ensuring all 
the users in our database are subscribed to our mailing list. Such a workload could be run in AWS Lambda, but we should 
prefer running it in AWS ECS on Fargate. 

We should prefer it because we already have secure connections to the data stores configured, and the code can be implemented
as a Rake task to benefit from the available application logic. The workload itself can use the same container image as
the application, which reduces the maintenance overhead.

We should strictly avoid using AWS Lambda for any workload that handles HTTP requests. The additional complexity and costs
(financial, organisational, and human) in our opinion massively outweigh any positives AWS Lambda has to offer.

## Consequences

The negative consequence of choosing AWS Lambda for certain types of workloads is that we have a second compute service in use 
within our infrastructure, which comes with the maintenance overhead associated with adopting any new service. 

Having a second compute service in use forever raises the question of where any given piece of code should run, however
we hope to mitigate that problem with the guidance given in this ADR.

We hope to mitigate the maintenance overheads of using AWS Lambda, such as updating language runtimes and dependency management, 
by including them in our existing processes for handling the same problems in AWS ECS on Fargate.

The positive consequence is that we have a low cost and relatively low maintenance path for running glue code within our
infrastructure.
