## GOV.UK Forms Account Creation on GOV.UK Signon

```mermaid
sequenceDiagram
  title GOV.UK Forms Account Creation on GOV.UK Signon
  actor user as GOV.UK Signon administrator
  participant browser as Web Browser
  participant signon as GOV.UK Signon
  link signon: signon Developer docs @ https://docs.publishing.service.gov.uk/repos/signon.html
  actor new_user as new GOV.UK Forms user

  user->>browser: visit GOV.UK Signon Users<br />https://signon.publishing.service.gov.uk/users
  browser->>signon: GET /users
  browser-->>user: show list of users

  alt User already exists
    user->>browser: click on user
    browser->>signon: GET /users/{user id}/edit
    user->>browser: check  GOV.UK Forms "Has access?", "Update User"
    browser->>signon: POST /users/{user id}
    signon-->>browser: 302
    browser->>signon: GET /users
  else User doesn't exist
    user->>browser: click on "Create User" button
    browser->>signon: GET /users/invitation/new
    user->>browser: Set name, Email, Normal Role, Organisation<br />check GOV.UK Forms "Has access?",<br />click "Create user and send email" button
    browser->>signon: POST /users/invitation
    signon->>new_user: "Please confirm your account" email
  end

```

## Accessing GOV.UK Forms via Signon

```mermaid
sequenceDiagram
  title Accessing GOV.UK Forms via Signon
  actor user as GOV.UK Forms user
  participant browser as Web Browser
  participant admin as forms-admin
  link admin: GitHub repo @ https://github.com/alphagov/forms-admin
  participant signon as GOV.UK Signon
  link signon: signon Developer docs @ https://docs.publishing.service.gov.uk/repos/signon.html

  user->>browser: visit GOV.UK Forms<br />https://admin.forms.service.gov.uk/
  browser->>admin: GET /
  admin-->>browser: 302
  browser->>admin: GET /auth/gds
  admin-->>browser: 302
  browser->>signon: GET /oauth/authorize?<br />client_id={client id}<br />&redirect_uri=https://admin.forms.service.gov.uk/auth/gds/callback<br />&response_type=code<br />&state={state}
  signon-->>browser: 302
  browser->>signon: GET /users/sign_in
  browser-->>user: show "Sign in to GOV.UK" page

  user->>browser: enter Email and Password, click "Sign in" button
  browser->>signon: POST /users/sign_in
  signon-->>browser: 302
  browser->>signon: GET /oauth/authorize?<br />client_id={client id}<br />&redirect_uri=https://admin.forms.service.gov.uk/auth/gds/callback<br />&response_type=code<br />&state={state}
  signon-->>browser: 302
  browser->>admin: GET /auth/gds/callback?<br />code={code}<br />&state={state}
  admin-->>browser: 302
  browser->>admin: GET /

  admin->>signon: ?
  signon-->>admin: ?

  browser-->>user: show GOV.UK Forms homepage
```

## Accessing GOV.UK Forms via Auth0

```mermaid
sequenceDiagram
    autonumber
    title Accessing GOV.UK Forms via Auth0
    actor user as unauthenticated user
    participant browser as web browser
    participant forms as GOV.UK Forms
    participant auth0 as Auth0
    participant gw as Google Workspace
    participant ses as Amazon SES

    user ->> browser: visit GOV.UK Forms
    browser ->> forms: HTTP GET
    forms ->> forms: no session cookie found
    forms -->> browser: redirect to /auth/auth0
    browser->> forms: HTTP GET


    note right of forms: using Auth0 OmniAuth strategy
    forms -->> browser: redirect to authorize
    browser ->> auth0: HTTP GET
    auth0 -->> browser: redirect to login
    browser ->> auth0: HTTP GET

    auth0 -->> browser: login screen
    browser -->> user: display login screen

    user ->> browser: provide email address
    browser ->> auth0: HTTP POST email address
    auth0 ->> auth0: check email address
    alt email address ends with "digital.cabinet-office.gov.uk"
      note over user: Google Workspace integration not yet implemented<br /><br />May use Home Realm Discovery (HRD)<br />or<br />seperate Auth0 connection flow
      auth0 ->> browser: redirect to Google Workspace
      browser ->> gw: HTTP GET
      opt If user doesn't have an active Google Workspace session
        gw -->> browser: login screen
        browser -->> user: display login screen
        user ->> browser: login
        browser ->> gw: HTTP POST
      end

      gw -->> browser: redirect to Auth0 callback

      browser ->> auth0: HTTP GET callback

    else all other email addresses
      auth0 ->> ses: use SES API
      ses ->> user: send one time code by email
      auth0 -->> browser: redirect to code entry screen
      browser ->> auth0: HTTP GET
      auth0 -->> browser: code entry screen
      browser -->> user: display code entry screen

      user ->> user: access email


      loop Until valid code provided
        user ->> browser: provide one time code
        browser ->> auth0: HTTP POST one time code

        auth0 ->> auth0: check code
      
        opt OTP incorrect
          auth0 -->> browser: Account blocked page
          note over user,browser: The code is not correct
        end

        opt Brute force protection
          auth0 -->> browser: Account blocked page
          note over user,browser: Your account has been blocked<br />after multiple consecutive login attempts
        end
      end
    end

      auth0 -->> browser: redirect to Auth0 resume
      browser ->> auth0: HTTP GET

      auth0 -->> browser: redirect to GOV.UK Forms with authorization code

    browser ->> forms: HTTP GET with authorization code
    forms ->> auth0: HTTP POST token request with authorization code
    auth0 -->> forms: ID token
    forms ->> forms: extract email address from ID token
    alt First time user has accessed GOV.UK Forms
        forms ->> forms: create record for user
    else Returning user
        forms ->> forms: get record of user
    end

    opt User has Super Admin role
      forms ->> forms: check user has authenticated with Google Workspace
    end

    forms ->> forms: create user session
    forms -->> browser: set session cookie, redirect
    browser ->> browser: store session cookie
    browser ->> forms: HTTP GET
    forms ->> forms: get list of forms
    forms -->> browser: 
    browser -->> user: display GOV.UK Forms

    note right of user: user is now authenticated

```
