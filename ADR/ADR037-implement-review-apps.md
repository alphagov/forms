# ADD037: Implement review apps in a new AWS account

Date: 2024-11-25

## Status
Proposed

## Context

### What are review apps?
Review apps are short-lived deployments of applications, based on a branch other than the main branch. They are often created automatically in response to a new pull request, and are kept up to date with the branch automatically. They are usually destroyed when the pull request is closed.

They exist to make it easy to create a live version of an application for review.

In the GOV.UK Forms context, deploying a review copy of one app will inherently mean deploying a short-lived copy of another, because we operate a microservice architecture.

### What are the limitations of review apps?

Review apps do not do everything that a full copy of an environment does, because they are a quick-to-deploy subset of a total subsystem. Common limitations of review apps include not being able to talk to systems beyond the immediate bounds of the application[^external-systems], and available data being strictly limited to a known, pre-populated set of test data.   

### Why do we want them

We want to introduce review apps on PRs to support both technical and non-technical team members in gaining access to a working version of the code in question. For non-technical team members, introducing review apps will make it possible for them to make changes and test changes (usually content changes) for themselves, without the support of a developer. For engineer team members, review apps will make it easier for them to test a subset of the system in a production-ish environment without needing to disturb the fully fledged development environment.

### What is in use elsewhere in GDS?

Other teams in GDS have faced the same issues as us. One particularly good example is the GOV.UK Design System team, who have a mix of technical and non-technical members. They host prototypes and review versions of applications on [Heroku](https://www.heroku.com/) using Heroku's [Review Apps](https://devcenter.heroku.com/articles/github-integration-review-apps) feature. This is also used on GOV.UK Forms among our content and interaction designers for hosting prototypes.

We investigated using Heroku Review Apps for our purposes, but we concluded that it was not a good choice. Heroku Review Apps is aimed at use cases involving a single application, but the applications we want to get review apps for will require deploying more than one application at a time.

## Decision

Implement Review Apps in a new AWS account using AWS CodeBuild Managed Self-Hosted GitHub Action Runners to deploy new and updated pull requests to ECS. Each Review App is accessed via  and routed to the correct container using Traefik.

### Workflow 

A developer (or non-technical team member) will raise a pull request for their change, and the system we build will deploy a review app in response to the opening of the pull request. The system will share a link to the running app in a comment on the pull request.

Subsequent changes to the pull request will result in the app being redeployed.

Once a reviewer has reviewed and merged the pull request, the system will destroy the running applications. 

### Architecture 
Given the workflow we want to have, and the investigations we have done, we have decided that we should build a review apps solution ourselves, using common services available to us in AWS.

We will run the review apps themselves as containers on AWS ECS on Fargate. The task definition we use will deploy containerised PostgreSQL alongside `forms-admin` and `forms-api`, and configure the apps to talk to the local database. This will ensure that the database in use for review apps is not shared between different instances of the review apps. [^seeding] 

As the interface between GitHub and our own AWS account, we will use [AWS CodeBuild self-hosted GitHub Action runners](https://aws.amazon.com/blogs/devops/aws-codebuild-managed-self-hosted-github-action-runners/). This is a feature of AWS CodeBuild which allows a GitHub Actions workflow to be run on AWS CodeBuild, inside your own AWS account, without needing to provide credentials to GitHub. [^risks] 

The GitHub Actions workflow will build containers and push them to a container registry in the account, and use Terraform to deploy those containers into AWS ECS on Fargate.

Traffic will reach the review apps over two hops:
1. An ALB will pass the HTTP request to a [Traefik](https://traefik.io/traefik/) proxy.
2. The Traefik proxy, configured to [discover routing information from AWS ECS](https://doc.traefik.io/traefik/routing/providers/ecs/), will forward the HTTP request onto the relevant container in ECS using host-name based routing.

Using a Traefik proxy will allow us to simplify the Terraform code needed to deploy a review app into AWS by removing the need to add and remove listeners from the ALB.

### Why not AWS CodePipeline

On GOV.UK Forms, we use AWS CodePipeline for continuous deployment through staging and into production and the user research environments. CodePipeline can be triggered in response to a pull request on GitHub, but we have decided against its use here.

Review apps are tightly tied to the pull request workflow, and we feel that the deployment of the review apps should work as similarly to other pull request checks we can make it. This means making use GitHub Actions workflows where possible. 

A secondary, useful benefit of using self-hosted GitHub Actions runners on CodeBuild is not needing to manage the GitHub access tokens. GitHub takes care of this on each invocation. If we were to use AWS CodePipeline, we would have to create, secure, and rotate the tokens in the pipeline ourselves.

### Limitations

The solution we've chosen has known limitations. Notably

1. There will be no access to external systems like GOV.UK Notify, or Sentry.
2. It will be unable to deploy a modified version of `forms-api` alongside a modified `forms-admin`. The version of `forms-api` in use will always be the latest version running in production.
3. There will be no live data to test with, only pre-generated seed data.

## Consequences

The decisions we've made about the architecture required for review apps on GOV.UK Forms have a small number of consequences:

* **6th AWS account**

  Prior to this we had 5 AWS accounts: development, staging, production, user-research, and deploy. We will add a 6th AWS to our collection: integration. The integration account will be used only for Review Apps at first, but its existence and the self-hosted GitHub Actions runner pattern we've established here can be reused for other things in the future.

* **Pull requests to `forms-admin` will result in a review app**

  All pull requests to `forms-admin` will trigger a new review app being created, and the closure of the PR will destroy the app. In future iterations we may make improvements like being able to opt out for a PR, or cost optimisation efforts like stopping very long-running applications (e.g. those of forgotten PRs)

  We intend to target only `forms-admin` in the first pass on this feature. Once we have had it running for `forms-admin` for a while, and had a chance to address any issues, we can make a second pass and extend it to `forms-runner`, `forms-api`, and `forms-product-page`.

* **Minor increase in AWS spend**

  All of these changes will result in an increase in our overall AWS spend. We will be careful in our implementation, but even so we expect the total cost of running review apps will be a small percentage of the production costs.


[^external-systems]: Here we mean both third-party systems, and systems within the environment that are not core to the application, for example an event bus that is not needed
[^seeding]: How we generate seed data in the database is out of scope for this ADR
[^risks]: Using self-hosted GitHub Actions runners presents us with a risk of malicious code running in a context with some level of privilege in an AWS account that we own. We will mitigate what we can by tightly controlling what permissions are granted to the runner, and whatever we cannot mitigate there we will manage with other mitigations.
