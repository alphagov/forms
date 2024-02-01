# ADR025: Decision Record Title (a description of the decision, not the problem)

Date: 2024-02-01

## Status

> Accepted or Rejected

## Context

Previously we added [PaperTrail](ADR013-use-paper-trail-gem-for-auditing-and-record-backups.md) with the intention to support reinstating from previous versions. We are not using it for that at all and we are not certain we're using it for the right models. Note that the previous ADR was added over a year ago.

Until we have a need for versioning, we should remove it from our code base to reduce complexity and code rot. We can easily re-add Papertrail when we get to implementing versioning.

## Decision

Remove Papertrail and clean up our code and database.

## Consequences
We will not be able to use PaperTrail to change a form from the `live_with_draft` state to the `live` state.

We will not be able to use PaperTrail for audit purposes.

We will need to implement a different way of determining if a user has been upgraded from a trial account to a full account. We currently check versions of a user and display a banner to them on their next login.
