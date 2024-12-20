## Uploading a file when completing a form

> [!NOTE]
> File upload has not yet been implemented, these are ideas / proposals:

```mermaid

---
title: GOV.UK Forms File Upload
---

sequenceDiagram

autonumber

actor user

participant browser

participant runner as forms-runner
participant s3 as Amazon S3
participant guard as Amazon GuardDuty
participant ses as Amazon SES
participant inbox as email inbox

actor processor

user->>browser: navigate to file upload page
browser->>runner: GET file upload page
runner->>runner: render file upload page
note over runner: can use "accept"<br />HTML attribute to<br />limit file type(s)
runner->>browser: HTTP response
browser->>user: display file upload page

note over user: users sees "File upload" component<br/>from GOV.UK Design System

user->>browser: select "Choose file"
browser->>user: display file dialog
user->>browser: select file
browser->>user: display filename of selected file
user->>browser: select "Continue"

browser->>runner: POST file
note over runner: Need to check memory requirements if holding files in memory

runner->>runner: check filesize
note over runner: is check done during upload or after upload?

note over runner: how to handle file size too big?

runner->>s3: write file
runner->>runner: associate file with user session

s3->>guard: new object event
note over guard: GuardDuty<br />Malware Protection<br />for S3
guard->>s3: scan

runner->>s3: GetObjectTagging
s3->>runner: return TagSet

note over runner: poll until tags returned

alt No malware detected
  guard->>s3: tag object NO_THREATS_FOUND
else otherwise
  guard->>s3: tag object
end

runner->>s3: GetObjectTagging
s3->>runner: return TagSet

note over user,guard: will user wait until file upload and checks have completed?

opt file not OK
  runner->>browser: redirect to error
  browser->>runner: GET file upload page with error (following redirect)
  runner->>browser: HTTP response
  browser->>user: display error message
  note over user: now what?<br />allow user to try again?
end

runner->>browser: redirect to next page
browser->>runner: GET next page (following redirect)
runner->>browser: HTTP reponse

note over user,runner: complete rest of questions

browser->>runner: GET check your answers
runner->>browser: HTTP response
browser->>user: display check your answers page

user->>browser: submit form
browser->>runner: POST submit form

note over runner: Also considering asynchronous email sending via queue

runner->>s3: get file(s)

note over runner: Need to check memory requirements if holding files in memory

runner->>ses: send email
alt success:
    ses->>inbox: send email
    runner->>browser: redirect to confirmation
    browser->>runner: GET confirmation page
    runner->>browser: HTTP reponse
    browser->>user: display confirmation page
    processor->>inbox: get form from inbox
    processor->>processor: process form
else failure:
    runner->>browser: redirect to error
    browser->>runner: GET error page
    runner->>browser: HTTP reponse
    browser->>user: display error page
    note over user: now what?<br />allow user to try again?
end
```

## Asynchronous form sending

> [!NOTE]
> File upload has not yet been implemented, these are ideas / proposals:

```mermaid

---
title: GOV.UK Forms Asynchronous form sending
---

sequenceDiagram

autonumber

participant runner as forms-runner
participant s3 as Amazon S3
participant ses as Amazon SES
participant inbox as email inbox

actor processor

runner->>runner: enqueue email sending job
note over runner: some time later...
runner->>runner: dequeue email sending job
runner->>s3: get file(s)
runner->>ses: send email
note over runner,ses: how are errors handled?
ses->>inbox: send email
processor->>inbox: get form from inbox
processor->>processor: process form

```
