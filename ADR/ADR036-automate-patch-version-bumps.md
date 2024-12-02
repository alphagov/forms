# ADR036: Automate patch version bumps

Date: 2024-10-31 :ghost:

## Status

Accepted

## Context

GOV.UK Forms uses [Dependabot](https://github.com/dependabot) to keep dependacies up to date. Dependency update pull requests are raised automatically by Dependabot but a human has to approve and merge the pull requests. This can be an issue because:
- we regularly have a large number of automated pull requests which require our attention. This means unnecessary toil, usually for the person on support
- security patches can go unnoticed for longer than we would like and they are only applied when we take action

A large number of PRs for a small team like that of GOV.UK Forms is not sustainable alongside other work, and being lax with
dependency updates and their security fixes is not something we should be doing.

### Semantice versioning
In general, the packages consumed by GOV.UK Forms conform to [semantic versioning](https://semver.org/) rules, which
allows us to make some assumptions about the changes introduced in a version change. In a semantically versioned package,
the patch version "MUST be incremented if only backward compatible bug fixes are introduced". By definition, we can
believe that if tests are passing after a patch version bump, then the change of version has had no negative impact.

Therefore, we can safely merge a PR for a patch version change once all of its status checks have passed.

Minor versions are similarly defined in the semantic versioning spec ("MUST be incremented if new, backward compatible
functionality is introduced to the public API."), however experience tells us that package authors more frequently
disrespect the specification for minor versions than patch versions, and as such minor and major version bumps are
out of scope for this ADR. A future ADR may address them.

## Risks
We have considered the risks outlined in the [Justification section in GOV.UK's rfc-167-auto-patch-dependencies](https://github.com/alphagov/govuk-rfcs/blob/main/rfc-167-auto-patch-dependencies.md#justification). In order to enable automatic patching in a repo it:

> MUST ensure it has sufficient security scanning  
MUST only be applied where there is no manual deployment step  
MUST ensure that branch protection rules are in place that prevent pushes to main if required status checks fail  
SHOULD ensure it has sufficient test coverage  
~~SHOULD~~MUST only automatically patch where the dependency version bump is patch ~~or minor~~  

Additionally, we agreed as a team that we:

- SHOULD not automatically bump minor patches for `npm` packages as we do not trust them to be non-breaking.
- MUST only apply automatic bump updates during working hours


### Sufficient security scanning

We currently use:
- [bundler-audit](https://github.com/rubysec/bundler-audit) for Software Composition Analysis (SCA) of bundler (it audits gems for security vulnerabilities)
- [Brakeman](https://brakemanscanner.org/) for Static Application Security Testing (SAST) of our Ruby on Rails applications. [As explained by the GOV.UK team](https://github.com/alphagov/govuk-rfcs/blob/main/rfc-167-auto-patch-dependencies.md#sufficient-security-scanning): Brakeman only scans "application source code - not the code of dependencies - for vulnerability signatures, so would not be very effective at catching dependency-related vulnerabilities" that are relevant to this ADR.

We could include:
- [npm-audit] or similar for Software Composition Analysis (SCA). Although we do not intend to automatically merge patch bumps for `npm` packages, this is a gap in our security scanning.

### No manual deployment step
We do not deploy any apps manually.

### Branch protection rules
We have branch protection enabled on the default branch (`main`) for our repos which require status checks to pass before merging. The checks include the security scan described earlier and a Continous Integration test suite as described below.

### Sufficient test coverage
We run unit tests in CI. Our test coverage is over 95% according to `rspec`.

Our end-to-end tests cover a form being "created, made live by form admin user and completed by a member of the public"

We have smoke tests for critical functionality (a member of the public completing and submiting a form)

### Merging updates during working hours
For our peace of mind, we will to only allow automatic merging of dependabot PRs during working hours (9am to 5pm, Monday to Friday). This way if there are any unexpected issues, an engineer can fix or revert the changes.

## Decision
We will automate merging patch version dependency bumps, as raised by Dependabot:
- between 9am and 5pm, Monday to Friday
- excluding `npm` related PRs

## Consequences
We will have to allow Github Actions to create and approve pull requests in our repos. We already allow "auto-merge"

We will have to run a Github action to [auto-approve](https://github.com/dependabot/fetch-metadata?tab=readme-ov-file#auto-approving) and [auto-merge patch updates](https://github.com/dependabot/fetch-metadata?tab=readme-ov-file#enabling-auto-merge)