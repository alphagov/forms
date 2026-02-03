# Sending submission emails asynchronously

forms-runner uses SolidQueue and Amazon SES/SNS to send submissions asynchronously.

## User submits their form

```mermaid

---
title: User submits their form
---

sequenceDiagram

autonumber

actor user as User

participant browser as Browser

participant runner as Forms Runner
participant runner-db as Forms Runner database
participant solidqueue-db as Solid Queue database

browser->>runner: GET check your answers
runner->>browser: HTTP 200 response
browser->>user: display check your answers page

user->>browser: select "Submit"
browser->>runner: POST submit form
runner->>runner-db: save Submission
runner->>solidqueue-db: enqueue send submission job

runner->>browser: HTTP 302 response
browser->>runner: GET confirmation page
runner->>browser: HTTP 200 response
browser->>user: Display confirmation page

```

## Sending the submission email asynchronously

```mermaid

---
title: Sending the submission email asynchronously 
---

sequenceDiagram

autonumber

participant worker as Forms runner worker
participant solidqueue-db as Solid Queue database
participant runner-db as Forms Runner database
participant s3 as Amazon S3
participant ses as Amazon SES
participant sns as Amazon SNS
participant inbox as Email inbox
participant sentry as Sentry

actor processor

worker->>solidqueue-db: dequeue send submission job
worker->>runner-db: get Submission
worker->>s3: get file(s)
worker->>ses: send email

break error 
  alt AWS SDK error and max retries not reached
    worker->>solidqueue-db: schedule retry
  else
    worker->>sentry: send error
  end
end

ses->>worker: return message_id
worker->>runner-db: set mail_message_id on Submission
worker->>runner-db: set the last_delivery_attempt timestamp on Submission

ses-)inbox: send email
note over ses,inbox: happens some time later

alt email sent successfully
  ses->>sns: send delivery notification
  processor->>inbox: get form from inbox
  processor->>processor: process form
else email bounces
  ses->>sns: send bounce notification
  note over ses,sns: We have an SQS queue subscribed to the<br/> SNS topic and a recurring task to poll<br/>the SQS queue.
end

worker->>worker: Recurring task deletes Submissions<br/> 30 days after they were created
```

## Handling email bounces/complaints
```mermaid

---
title: Handling email bounces/complaints
---

sequenceDiagram

autonumber

participant worker as Solid Queue worker
participant solidqueue-db as Solid Queue database
participant runner-db as Forms Runner database
participant sqs as Amazon SQS
participant sentry as Sentry

actor support as Forms team tech support

worker->>solidqueue-db: enqueue recurring receive bounces job
worker->>solidqueue-db: dequeue receive bounces job
worker->>sqs: get messages from bounces and complaints queue
alt there is a bounce SQS message
  worker->>runner-db: get Submission by the message_id in the SQS message
  worker->>runner-db: update delivery_status of Submission to "bounced"
  worker->>worker: Log with the submission details
  worker->>sentry: send error event
  sentry->>support: Alert via Slack
  support->>support: Identify why the email bounced
  support->>support: Run rake task to retry submission
else there is a complaint SQS message
  worker->>runner-db: get Submission by the message_id in the SQS message
  worker->>worker: Log with the submission details
end

```

## Handling successful deliveries

```mermaid

---
title: Handling successful deliveries
---

sequenceDiagram

autonumber

participant worker as Solid Queue worker
participant solidqueue-db as Solid Queue database
participant runner-db as Forms Runner database
participant sqs as Amazon SQS

actor support as Forms team tech support

worker->>solidqueue-db: enqueue recurring receive deliveries job
worker->>solidqueue-db: dequeue receive deliveries job
worker->>sqs: get messages from deliveries queue
worker->>runner-db: get Submission by the message_id in the SQS message
worker->>worker: log a "form_submission_delivered" event
note over worker,runner-db: we don't currently use the "delivered" status for anything other than for information
```
