# Completed form submissions

## Contents

- [What](#what)
- [Iterations](#iterations)
___

## What

How completed forms are sent to the form owners for processing, and how form creators set this up in the platform. 

## Iterations

### Email submissions

The initial MVP of the form builder provided email as the only way to receive completed form submissions. 

The form creator has to provide an email address for them to be sent to. That email address must be verified with a code before it can receive submissions. This must be done before a form can be made live. 

When a form is completed, the answers given are sent to the email address in the body of an email. There is one email for each form completed.  

Email was the starting point for the product as it is equivalent to the way many document-based forms are delivered to government services. 

### CSV file email attachment

This iteration added the option for form creators to also get the answers in a CSV file attached to each completed form email. The task list to create or edit a form was given an extra optional task to 'Get completed forms as CSV files' for form creators to turn the CSVs on or off.

### [JSON file email attachment, December 2024](version-3-json-submissions.md)

This added the option for form creators to get form submissions in a JSON file attached to each completed form email. 

### S3 buckets, late 2024

We offered teams the option to set up AWS S3 buckets to receive completed form submissions. Initially this was offered as a manual process outside of the platform.
The form owners would have to set up the bucket and manage it themselves. They would also have to choose to receive completed forms as either JSON or CSV files. Once we set it up, they would then get completed forms sent to their S3 bucket instead of via email. 
