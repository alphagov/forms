# ADR036: Automate patch version bumps

Date: 2024-10-31 :ghost:

## Status

Proposed

## Context

GOV.UK Forms uses [Dependabot](https://github.com/dependabot) to keep dependacies up to date. Dependancy update pull requests are raised automatically by Dependabot but a human has to approve and merge the pull requests. This can be an issue because:
- we regularly have a large number of automated pull requests which require our attention. This means unnecessary toil, usually for the person on support
- security patches can go unnoticed for longer than we would like and they are only applied when we take action

A large number of PRs for a small team like that of GOV.UK Forms is not sustainable alongside other work, and being lax with
dependency updates and their security fixes is not something we should be doing.

### Semantice versioning
In general, the packages consumed by GOV.UK Forms conform to [semantic versioning](https://semver.org/) rules[2], which
allows us to make some assumptions about the changes introduced in a version change. In a semantically versioned package,
the patch version "MUST be incremented if only backward compatible bug fixes are introduced". By definition, we can
believe that if tests are passing after a patch version bump, then the change of version has had no negative impact.

Therefore, we can safely merge a PR for a patch version change once all of its status checks have passed.

Minor versions are similarly defined in the semantic versioning spec ("MUST be incremented if new, backward compatible
functionality is introduced to the public API."), however experience tells us that package authors more frequently
disrespect the specification for minor versions than patch versions, and as as such minor and major version bumps are
out of scope for this ADR. A future ADR may address them.

### Risks
See the [Justification section in GOV.UK's rfc-167-auto-patch-dependencies](https://github.com/alphagov/govuk-rfcs/blob/main/rfc-167-auto-patch-dependencies.md#justification)


## Decision
We will automate merging patch version dependancy bumps, as raised by Dependabot


## Consequences
We will have to allow Github Actions to create and approve pull requests in our repos. We already allow "auto-merge"

We will have to run a Github action to [auto-approve](https://github.com/dependabot/fetch-metadata?tab=readme-ov-file#auto-approving) and [auto-merge patch updates](https://github.com/dependabot/fetch-metadata?tab=readme-ov-file#enabling-auto-merge)