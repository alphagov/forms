# ADR037: Use Amazon S3 and GuardDuty Malware Protection for file upload

Date: 2024-12-04

## Status

Proposed

## Context

Sometimes users need to upload a file as part of completing a form. These files need to be stored temporarily until the form is sent to the receiving organisation. It's possible that uploaded files may contact malware, so they should be checked first before send them on.

## Decision

Store uploaded files in [Amazon S3](https://aws.amazon.com/s3/), and enable [GuardDuty Malware Protection for S3](https://docs.aws.amazon.com/guardduty/latest/ug/gdu-malware-protection-s3.html) to check for malware.

## Consequences

A new S3 bucket needs to be created which `forms-runner` can access.

There is a cost associated with the use of GuardDuty Malware Protection, [$0.95 per GB per month in Europe (London) Region](https://aws.amazon.com/guardduty/pricing/#GuardDuty_protection_plans) as of December 2024.

Files uploaded to S3 must be deleted when the user session they are associated with ends / expires.
