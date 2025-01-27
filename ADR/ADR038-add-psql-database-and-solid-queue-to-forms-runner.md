# ADR038: Store submission data in PostgreSQL and use Solid Queue to send emails asynchronously

Date: 2024-11-25

## Status

Approved

## Context

Forms will be using AWS SES to deliver emails to form processors with files attached to the emails.

For our team to successfully process submission emails we must have:

* a queuing mechanism to send emails asynchronously
* a way to retry the email on failed submissions, for example if an email bounces.

### Sending emails asynchronously

When the user uploads a file when they are completing a form we will store the file in S3. When they submit their form, we need to download any files they have uploaded from S3 to include in the attachment. If we do this synchronously at the point the user clicks the submit button, this will take some time to process, resulting in the user having to wait on the submission page until this is completed which is a poor user experience. This also has the potential to block our handling of other incoming HTTP requests to the Runner app if we are processing multiple email submissions with large attachments at the same time, impacting service performance and availability.

### Handling bounced emails

When an API request is made to AWS SES to send an email, if there isn't an error, then the email is queued for sending. At this point we cannot be sure that the email will make it to the form processor's inbox - the email may still bounce.

In SES, we can configure an SNS topic to receive notifications about bounces and complaints, as well as for successful delivery. These notifications contain metadata about the email, but AWS does not store the email content for us to retrieve. In the case that an email bounces, we need to be sure that we have not lost the submission data, as we receive the notification about a bounce some time after we have told the form filler that their form was successfully submitted. This means we need to store the submission data at least until we have can be sure that the email hasn't bounced.

## Proposed implementation

### Queuing mechanism to send emails asynchronously

We looked at 3 options for the queueing mechanism:

* Sidekiq
* Solid Queue
* SQS

#### Sidekiq

Sidekiq is a Ruby library for processing background jobs, with queues backed by Redis. This is a commonly used solution for running background jobs for Rails apps, which is why we considered it - along with the fact that our Forms Runner app already uses Redis.

The issue that we found with this was that due to the way Sidekiq uses Redis in the free version is it possible for it to lose jobs if the process crashes. [GOV.UK solved this problem](https://github.com/alphagov/email-alert-api/blob/7dd5cc5235ec42708c9dce14de51bd40e2b3cd77/docs/adr/adr-009-sidekiq-lost-job-recovery.md) by storing data required to process the job in a database, and having another process to check that jobs have completed. There is a pro version of Sidekiq which adds additional guarantees that jobs won't be lost but this costs a significant amount.

#### Solid queue

Solid Queue, which is a queue backed by a SQL database, is the default for ActiveJob in Rails 8. This provides us a guarantee that jobs are only run once and will not be lost, as it works by locking a database row for reads while it is processing a job and only deleting the database row after the job has successfully completed. Solid Queue provides automatic retries for jobs, and it is possible to configure an out-of-the box administrative dashboard using the `mission_control-jobs` gem to view and manage jobs.

We can use Solid Queue with a PostgreSQL database that we set up in AWS, which we already have running for other parts of the system.

The need for a SQL database isn't a blocker to using Solid Queue, as we need to add a database to store submission data to handle bounced email anyway, as outlined [below](#storing-submission-data-to-handle-bounced-emails).

##### Pros

* Solid Queue is the Rails default, and is well supported.
* We think that it should be easy to configure the initial setup.
* It's easy to run Solid Queue on a developer machine for local testing.
* It's easy to configure recurring tasks. We think we'll need to run a recurring task to delete submission data when our retention period has elapsed.

##### Cons

* We need to put more thought into how we add useful monitoring and alerting.
* Extra configuration is required to set up a job management dashboard.

#### AWS SQS

It is possible to set up SQS to work with ActiveJob which will manage queueing and processing background jobs. SQS has automatic retries and dead letter queues which would allow us to handle cases where we fail to initiate sending the email. We could use FIFO SQS queues to guarantee that jobs are only processed once, and so we do not send duplicate emails.

As we need to store data in a database to [handle bounced emails](#storing-submission-data-to-handle-bounced-emails), the message size limit of 256 KB will not be an issue for us. We can just send an ID referencing the submission in the SQS message. The cost associated with sending the number of SQS messages that we anticipate is negligible.

There is an AWS gem, `aws-activejob-sqs-ruby` to integrate SQS with ActiveJob in Rails. However, this is not widely used.

##### Pros

* We already use SQS for bounce notifications for SES emails.
* Lots of the team are familiar with SQS.
* We know how to set up alerts for messages going into the dead letter queue, and if the queue gets too big.

##### Cons

* The Ruby gem to use ActiveJob to queue tasks using SQS isn't widely used.
* To test running background jobs on a developer machine we'll need additional setup to connect to AWS or run an SQS mock locally.

#### Chosen technology

We have decided to use ActiveJob backed by Solid Queue to send emails asynchronously. This is because this is the default way of processing background jobs in Rails and we think it should be fairly straightforward to configure, and run locally for testing. As we require a SQL database for storing submission data, needing a database is not a blocker to using Solid Queue. However, when making this decision we thought the pros and cons of Solid Queue and SQS were quite balanced. Therefore, we're open to switching to using SQS if there are difficulties we spot using Solid Queue or additional advantages of using SQS that become apparent.

### Storing submission data to handle bounced emails

When we receive a notification via AWS SNS about a bounced email, the message contains metadata about the email we attempted to deliver including the `message_id`. In order to handle a bounced email and attempt to re-send it we need to match up the `message_id` to the submission data. This ADR proposes to store the submission data in a database table when the user submits their form. Then at the point we make the API request to SES to send the email and receive a success response, we would store the `message_id` against the submission.

Submission data would be kept in the database until we are sure the email has not bounced. We should be able to receive notifications about successful deliveries to an SNS topic, although further investigation is required into the reliability of this mechanism. We can either delete the data when we receive notification of a successful delivery, or when sufficient time has passed and we have not received a bounce/complaint notification. Forms Runner will need a background job to poll SQS queues subscribed to these SNS topics if we want to perform actions for these events. It makes sense to use ActiveJob to run a recurring task to do this.

Adding a database now will allow for other features down the line. In particular, storing submission data in a database will likely be required when we implement the ability for form fillers to save their data and return later.

It makes most sense for us to store submission data in a PostgreSQL database, as this provides reliable storage that is easily accessible and we already use PostgreSQL for other microservices.

We have some concerns about database performance if we use the same Amazon Aurora instance for databases for all of our microservices. One app seeing increased request volumes places increased load on the database, which can degrade the performance of the other apps as the database slows. We also have some concerns about database restoration/roll back if all apps use the same Aurora instance. If this were the case we can only rollback databases for all our apps. The risk of losing submission data if this were to happen is a major concern. For these reasons we want to add a separate Aurora cluster for the Forms Runner database.

We should consider encrypting the submission data at rest in the database, if we think that this adds worthwhile protection.

## Decision

We will use Solid Queue and ActiveJob to manage the background processing of emails.

We will use PostgreSQL/RDS for the database on the Forms Runner, with a separate Aurora instance.

## Consequences

We will have a reliable way to deliver emails to form processors with files attached to the emails.

Forms Runner will be responsible for running background jobs to send submission emails and consume SQS messages that inform us about the send result. We will have to manage any performance impacts of this and configure additional monitoring.

We have an additional infrastructure dependency on PostgreSQL for Forms Runner. There will be additional costs to configuring another Amazon Aurora instance. We also want to bring forward work to allow for zero downtime RDS updates so that we don't need to make the platform unavailable for form fillers whilst performing an update.
