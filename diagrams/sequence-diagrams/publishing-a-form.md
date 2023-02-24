# Making a form live

```mermaid 
sequenceDiagram
  title Previewing a form
  actor user as form creator
  participant browser as Web Browser
  participant admin as forms-admin
  link admin: GitHub repo @ https://github.com/alphagov/forms-admin   
  participant api as forms-api
  link api: GitHub repo @ https://github.com/alphagov/forms-api  

  note right of user: All tasks except "Make your form live" have been completed

  admin-->>user: show "Create a form" page
  user->>browser: Click "Make your form live" link
  browser->>admin: GET /forms/{form id}/make-live
  admin->>api: GET /api/v1/forms/{form id}
  admin->>api: GET /api/v1/forms/{form id}
  browser-->>user: show "Make your form live" page

  user->>browser: Confirm making form live<br />click "Save and continue" button
  browser->>admin: POST /forms/{form id}/make-live
  admin->>api: GET /api/v1/forms/{form id}
  admin->>api: GET /api/v1/forms/{form id}
  admin->>api: GET /api/v1/forms/{form id}/pages
  admin->>api: POST /api/v1/forms/{form id}/make-live<br>payload: {includes all form attributes and values}<br>Controller Action doesn't use any
  admin-->>browser: REDIRECT 302
  browser->>admin: GET /forms/{form id}/live-confirmation
  admin->>api: GET /api/v1/forms/{form id}
  admin->>api: GET /api/v1/forms/{form id}
  browser-->>user: show "Your form is live" page
  user->>user: Copy URL for the form

```

# Publishing a form

```mermaid 
sequenceDiagram
  Title Publishing a form
  actor user as Form creator
  actor content as Content Designer
  participant publishing as GOV.UK Publishing tools
  participant govuk as GOV.UK website

  note right of user: Form has been made live

  user->>content: Provide form URL

  content->>publishing: Edit existing page or create new page<br />Link to form URL

  publishing->>govuk: Publish new content

```
