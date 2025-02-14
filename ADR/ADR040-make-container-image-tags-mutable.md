# ADR040: Make container image tags mutable

Date: 2025-02-12

## Status

Accepted

## Context

At the time of writing, we use [Amazon ECR](https://aws.amazon.com/ecr/) to host our container image repositories. 

Each container image can have any number of tags applied to it, consistent with [the Open Container Initiative spec](https://github.com/opencontainers/distribution-spec/blob/main/spec.md). No two container images can have the same tag, and attempting to apply the same tag to a second image will result in an error. This is called tag immutability, and is [a feature of AWS ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-tag-mutability.html) that we have enabled.

The alternative to tag immutability is tag mutability. With tag mutability enabled, when a tag is applied to a second container image, the tag is removed from the first one before being applied to the second. It is, in effect, a move operation. In most cases this is an undesirable property of an image repository, because it allows for situations where downloading a container image with a given tag on two occasions can result in different images; you can never be absolutely sure that you got the same bytes twice.

We are implementing review applications for `forms-admin` (see [ADR037](./ADR037-implement-review-apps.md)). In our implementation we want to deploy the version of `forms-admin` under review alongside the latest production version of `forms-api`. Deploying the latest production version means two things:

1. we don't need to constantly update the code to change the version being deployed
2. we need a mechanism for consistently identifying the latest production version

The `latest` tag is conventionally the tag used to denote the most recent version of a container image, or otherwise the latest production-ready image. We see no reason not to follow convention, and have begun [tagging the newest production-ready images](https://github.com/alphagov/forms-deploy/pull/1346). 

However, this isn't actually possible without enabling tag mutability within our container repositories, because we are moving the `latest` tag between images. 

## Decision

We have decided to enable tag mutability for our container repositories in [Amazon ECR](https://aws.amazon.com/ecr/).

## Consequences

There are two consequences of this decision

1. we are able to move the `latest` tag between container images
2. we can, in theory, encounter situations where downloading an image with a tag other than `latest` on two occasions can result in different bytes

However, we don't think that consequence two will play out in practice for a number of reasons. 

First, our convention for application image tagging is to include both the git commit hash for the source code and the timestamp of when it was built. This always results in unique tags. 

Second, our applications are always deployed with a specific tag in our conventional format. We never deploy `latest` to production. 

Lastly, we have strong access controls in place for AWS to prevent malicious actors from gaining access and moving the tags about. The insider threat is a known risk, and insiders actions will always appear in an audit trail.
