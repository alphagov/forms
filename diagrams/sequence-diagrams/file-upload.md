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

alt If file is uploaded to forms-runner
  browser->>runner: POST html form data
  runner->>s3: write file
  runner->>browser: redirect
else If file is uploaded directly to S3
  note over browser, s3: See https://docs.aws.amazon.com/AmazonS3/latest/API/sigv4-UsingHTTPPOST.html
  browser->>s3: POST html form data
  alt If successful
    note over browser, s3: what HTTP response code is used?
    s3->>browser: redirect
  else If error
    note over browser, s3: "If the upload fails, Amazon S3 displays an error and does not redirect the user to a URL."<br />unclear how to handle this error scenario...
    s3->>browser: HTTP response
    browser->>user: display Amazon S3 error
    note over user: ?!
  end
end

s3->>guard: new object event
note over guard: GuardDuty<br />Malware Protection<br />for S3
guard->>s3: scan

alt No malware detected
  guard->>s3: tag object NO_THREATS_FOUND
else otherwise
  guard->>s3: tag object
end

browser->>runner: GET (following redirect)
runner->>s3: GetObjectTagging
s3->>runner: return TagSet

note over user,guard: will user wait until file upload and checks have completed?

alt file OK
  runner->>runner: render success
  runner->>browser: HTTP response
else file not OK
  runner->>runner: render error
  runner->>browser: HTTP response
  browser->>user: show error message
  note over user: now what?
end

user->>browser: navigate to next question
browser->>runner: GET next question

note over user,runner: complete rest of questions

runner->>browser: check your answers
note over browser: what happens if file(s) haven't been scanned yet?

user->>browser: submit form
browser->>runner: submit form
runner->>s3: get file(s)
runner->>ses: send email
ses->>inbox: send email
```
