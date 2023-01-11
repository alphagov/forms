## Creating a form

```mermaid
sequenceDiagram
  title Creating a new form
  actor user as form creator
  participant browser as Web Browser
  participant admin as forms-admin
  link admin: GitHub repo @ https://github.com/alphagov/forms-admin
  participant api as forms-api
  link api: GitHub repo @ https://github.com/alphagov/forms-api

  note right of user: user has already logged in

  user->>browser: click "Create a form >" button
  browser->>admin: GET /forms/new
  browser-->>user: show "What is the name of your form?" page
  user->>browser: Give the form a name<br />click "Save and continue" button
  browser->>admin: POST /forms/new<br />payload: forms_change_name_form%5Bname%5D={form name}
  admin->>api: POST /api/v1/forms<br />{"name":"{form name}",<br />"submission_email":"",<br />"org":"{user orginisation}"}
  api->>api: Create form
  api-->>admin: {"id":{form id}}
  admin-->>browser: 302
  browser->>admin: GET /forms/{form id}
  Note right of admin: unclear why this next request happens twice, but it does
  admin->>api: GET /forms/{form id}
  admin->>api: GET /forms/{form id}
  admin->>api: GET /forms/{form id}/pages
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
  participant api as forms-api
  link api: GitHub repo @ https://github.com/alphagov/forms-api

  note right of user: On the "Create a form" page

  user->>browser: click "Add and edit your questions" link
  browser->>admin: GET /forms/1/pages/new/type-of-answer
  Note right of admin: unclear why this next request happens twice, but it does
  admin->>api: GET /forms/{form id}
  admin->>api: GET /forms/{form id}
  admin->>api: GET /forms/{form id}/pages

  browser-->>user: show "What kind of answer do you need to this question?" page

  user->>browser: Select a question type<br />click "Save and continue" button

  note right of browser: multiple steps to select question type

  browser->>admin: GET /forms/{form id}/pages/new
  browser-->>user: show "Edit question" page


  user->>browser: Provide Question text, Hint text (optional), Question settings
  user->>browser: Click "Save and add next question" OR "Save question" button
  browser->>admin: POST /forms/{form id}/pages/new
  admin->>api: POST /forms/{form id}/pages<br />{"question_text":,<br />"hint_text":,<br />"answer_type":,<br />"is_optional":,<br />"answer_settings":{"input_type":}
  api->>api: create page
  api-->admin: { ??? }

  alt "Save and add next question" clicked
    admin-->>browser: 302
    browser->>admin: GET /forms/1/pages/new/type-of-answer
    browser-->>user: show "What kind of answer do you need to this question?" page 
  else "Save question" clicked
    admin-->>browser: 302
    browser->admin: GET /forms/{form id}/pages/2/edit
    browser-->>user: show "Edit question" page
  end
```

## Set other form details

TODO


## Set email address for completed forms

TODO

## Previewing a form

TODO