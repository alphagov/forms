# ADR047: Compute submission status from delivery timestamps

Date: 2025-12-04

## Status

Proposed

## Context

We are making submission delivery asynchronous for all submission methods (email and S3) and we need a more robust way to track the delivery status of submissions in forms-runner.

### Using the Submission model for all submission types

To make S3 submissions asynchronous, we need to use the `Submission` model for S3 submissions. Currently, only email submissions create `Submissions`. The model only supports `pending` or `bounced` values for the `delivery_status` enum - there is no `delivered` status. This would make it difficult for S3 submission to use the `Submission` model, as we would need a way see which Submission are successful versus those that may need to be retried.

### Handling race conditions with async notifications

For email submissions, delivery and bounce notifications are processed asynchronously. This creates a race condition: we may receive and process these notifications out of order. Using timestamps for `delivered_at` and `bounced_at` allows us to accurately determine the sequence of events. We can only mark a submission as `delivered` if we can confirm that any bounce notification didn't occur after the successful delivery notification (i.e. an async bounce).

## Decision

We will replace the fixed `delivery_status` enum attribute with a computed `status` method that derives the submission status from `delivered_at` and `bounced_at` timestamp columns.

The implementation will proceed in three phases:

1. **Add new timestamp column**: Add the `bounced_at` attribute to the `Submission` model via a database migration (the `delivered_at` column already exists).

2. **Switch to computed status**: Replace usage of `delivery_status` with the computed `status` method throughout the codebase. The `status` method will return one of three values:
   - `:pending` - when both `delivered_at` and `bounced_at` are nil
   - `:delivered` - when `delivered_at` is present and either `bounced_at` is nil or `delivered_at` is more recent
   - `:bounced` - when `bounced_at` is present and either `delivered_at` is nil or `bounced_at` is more recent

The 'delivered_at' and 'bounced_at' should represent the most recent delivery attempt. I.e. set to nil when a new delivery attempt is made.

3. **Remove legacy column**: Remove the `delivery_status` enum attribute and its database column.

## Consequences

### Positive

- S3 submissions can use the Submission model. Adding a `delivered` status enables S3 submissions to use the same `Submission` model as email submissions, allowing us to easily see successful deliveries and those that need to be retried. This ultimately allows us to make S3 submissions asynchronous.

- Correct handling of async bounce notifications. Timestamps allow us to accurately determine submission status even when delivery and bounce notifications are processed out of order.

- Simplified logic for Submission deletion and retry. Determining which submissions to delete (those with `delivered` status) instead of finding "not_bounced" or assuming those that are "pending" are "delievered".

- Provides an audit trail. Timestamps record when state changes occurred, providing more context than a single enum value.

### Negative

- Requires more complicated (and potentially slower) database queries to find delivered and bounced submissions. Not likely to cause issues out our current scale.
