## Creating a form

```mermaid
sequenceDiagram
  title Creating a new form
  actor user as form creator
  participant browser as Web Browser
  participant admin as forms-admin
  link admin: GitHub repo @ https://github.com/alphagov/forms-admin

  note right of user: user has already logged in

  user->>browser: click "Create a form >" button
  browser->>admin: GET /forms/new
  browser-->>user: show "What is the name of your form?" page
  user->>browser: Give the form a name<br />click "Save and continue" button
  browser->>admin: POST /forms/new<br />payload: forms_change_name_form%5Bname%5D={form name}
  admin->>admin: Create form
  admin-->>browser: 302
  browser->>admin: GET /forms/{form id}
  browser-->>user: show "Create a form" page
```

## Adding the first question

```mermaid
sequenceDiagram
  title Adding the first question
  actor user as form creator
  participant browser as Web Browser
  participant admin as forms-admin
  link admin: GitHub repo @ https://github.com/alphagov/forms-admin

  note right of user: On the "Create a form" page

  user->>browser: click "Add and edit your questions" link
  browser->>admin: GET /forms/1/pages/new/type-of-answer

  browser-->>user: show "What kind of answer do you need to this question?" page

  user->>browser: Select a question type<br />click "Save and continue" button

  note right of browser: multiple steps to select question type

  browser->>admin: GET /forms/{form id}/pages/new/question
  browser-->>user: show "Edit question" page


  user->>browser: Provide Question text, Hint text (optional), Question settings
  user->>browser: Click "Save and add next question" OR "Save question" button
  browser->>admin: POST /forms/{form id}/pages/new/question
  admin->>admin: create page

  alt "Save and add next question" clicked
    admin-->>browser: 302
    browser->>admin: GET /forms/1/pages/new/type-of-answer
    browser-->>user: show "What kind of answer do you need to this question?" page 
  else "Save question" clicked
    admin-->>browser: 302
    browser->admin: GET /forms/{form id}/pages/2/edit/question
    browser-->>user: show "Edit question" page
  end
```

## Set other form details

```mermaid
sequenceDiagram
  title Set other form details
  actor user as form creator
  participant browser as Web Browser
  participant admin as forms-admin
  link admin: GitHub repo @ https://github.com/alphagov/forms-admin

  note right of user: form already created

  user->>browser: click "Add a declaration for people to agree to" link
  browser->>admin: GET /forms/{form id}/declaration

  browser-->>user: show "Add a declaration" page
  user->>browser: Provide declaration<br />click "Save and continue" button
  browser->>admin: POST /forms/{form id}/declaration
  admin->>admin: Update form
  admin-->>browser: 302
  browser->>admin: GET /forms/{form id}
  browser-->>user: show "Create a form" page
```

Diagram shows "declaration". Flow is equivalent for

* what-happens-next
* privacy-policy
* contact-details

## Set email address for completed forms

```mermaid
sequenceDiagram
  title Set other form details
  actor user as form creator
  participant browser as Web Browser
  participant admin as forms-admin
  link admin: GitHub repo @ https://github.com/alphagov/forms-admin
  participant notify as GOV.UK Notify
  participant inbox as shared email inbox
  actor processor as form processor

  note right of user: form already created

  user->>browser: click "Set the email address for completed forms" link
  browser->>admin: GET /forms/{form id}/submission-email
  browser-->>user: show "Set the email address for completed forms" page
  user->>browser: Provide email address<br />click "Save and continue" button
  browser->>admin: POST /forms/{form id}/submission-email
  admin->>admin: Generate and store confirmation_code
  admin->>notify: Send email with confirmation_code
  notify->>inbox: Send email
  admin-->>browser: 302
  browser->>admin: GET /forms/{form id}/email-code-sent
  browser-->>user: show "Confirmation code sent" page

  inbox--)processor: read email
  processor--)user: provide confirmation_code

  user->>browser: click "Enter the email address confirmation code" link
  browser->>admin: GET /forms/{form id}/confirm-submission-email
  browser-->>user: show "Enter the confirmation code" page 

  user->>browser: enter code, click "Save and continue" button
  browser->>admin: POST /forms/{form id}/confirm-submission-email
  admin->>admin: check code

  opt wrong code entered
    admin-->>browser: 200
    browser-->>user: show "Enter the confirmation code" page with error
    user->>browser: enter code, click "Save and continue" button
    browser->>admin: POST /forms/{form id}/confirm-submission-email
    admin->>admin: check code
  end

  admin->>admin: update form
  admin-->>browser: 302
  browser->>admin: GET /forms/{form id}/submission-email-confirmed
  browser-->>user: show "Email address confirmed" page
```

## Previewing a form

```mermaid 
sequenceDiagram
  title Previewing a form
  actor user as form creator
  participant browser as Web Browser
  participant admin as forms-admin
  link admin: GitHub repo @ https://github.com/alphagov/forms-admin  
  participant runner as forms-runner
  link runner: GitHub repo @ https://github.com/alphagov/forms-runner  

  note right of user: At least one question has been added

  admin-->>user: show "Create a form" page
  user->>browser: Click "Preview this form in a new tab" link
  browser->>runner: GET /preview-form/{form id}/{form slug}
  runner->>runner: determine start page  
  runner-->>browser: 302
  browser->>runner: GET /forms/{form id}/{form slug}/{start page id}
  runner-->>browser: render form start page
  browser-->>user: show form preview in new tab
```
