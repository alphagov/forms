# ADR041: Grant review apps workflow pull request write access

Date: 2025-02-19

## Status

Accepted

## Context

We have built a GitHub Actions [workflow for deploying review apps](https://github.com/alphagov/forms-admin/blob/main/.github/workflows/review_apps_on_pr_change.yml) for pull requests in `forms-admin`.  As part of that workflow we want to leave a comment on the PR to say that a review app has been deployed, and provide the URL.

Our GitHub organisation's default permission level for GitHub Actions is read-only, and we must explicitly add additional permissions in our workflows.

In GitHub's security model, leaving a comment on a pull request requires write access to pull requests. This level of access also enables a user to create, merge, and close PRs.

Being able to create and merge PRs in the repository programmatically opens us up to a malicious actor doing something along the lines of

1. Raise a PR which targets the review apps workflow
1. Use the write access of that workflow to raise a new PR with malicious code
1. Use the write access of the first PR to merge the second PR, resulting in the code eventually reaching production.

We believe we have sufficient mitigations in place to reduce the likelihood of the above vulnerability being exploited

### Limited human write access to the repository

Only members of the GOV.UK Forms team have write access to the repository, granted as part of the onboarding process. Other people within GDS have no write access.

### Pull requests from forked repositories do not trigger workflows

In GitHub, we have configured workflows to require approval to run on pull requests coming from forked repositories. Approval must come from a human with write access to the repository.

### Pull requests require approval before merging

In GitHub, we have required a minimum of one human approval to be given before a pull request can be merged. This can be bypassed, but only by a limited number of people on the team.

### Pull requests require certain checks to be passing before merging

In GitHub, we have required a small number of checks in other GitHub Actions workflows to be passing before a PR can be merged. When a pull request is raised from within GitHub Actions, workflows are not automatically run for it. This means those checks cannot be passing without human intervention.

> When you use the repository's GITHUB_TOKEN to perform tasks, events triggered by the `GITHUB_TOKEN`, with the exception of `workflow_dispatch` and `repository_dispatch`, will not create a new workflow run. This prevents you from accidentally creating recursive workflow runs. For example, if a workflow run pushes code using the repository's `GITHUB_TOKEN`, a new workflow will not run even when the repository contains a workflow configured to run when `push` events occur.

https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/triggering-a-workflow#triggering-a-workflow-from-a-workflow

## Decision

We have decided we will grant the review apps workflow write access to pull requests. As an additional measure, in our GitHub repository configuration we will remove the permission for GitHub Actions to create pull requests or submit approvals.

## Consequences

As a consequence of granting one workflow write access to pull requests, we expose the vulnerability documented above.

We also gain the ability to leave comments on PRs from the one workflow.
