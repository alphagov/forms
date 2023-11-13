## Accessing GOV.UK Forms via Auth0

```mermaid
sequenceDiagram
    autonumber
    title Accessing GOV.UK Forms via Auth0
    actor user as unauthenticated user
    participant browser as web browser
    participant forms as GOV.UK Forms
    participant auth0 as Auth0
    participant auth0-ui as Auth0 Universal Login
    participant ses as Amazon SES

    user ->> browser: visit GOV.UK Forms
    browser ->> forms: HTTP GET
    forms ->> forms: no _forms_admin_session cookie from client (or user id or auth_timestamp older than 24 hours)
    note right of forms: using Auth0 OmniAuth strategy
    forms -->> browser: redirect to /auth/auth0, set _forms_admin_session cookie
    browser ->> forms: HTTP GET /auth/auth0
    forms -->> browser: redirect to auth0-tenant/authorize
    browser ->> auth0: HTTP GET
    auth0 -->> browser: redirect to Universal login
    browser ->> auth0-ui: GET /u/login/
    auth0-ui -->> browser: Login page
    browser -->> user: display login screen

    user ->> browser: provide email address
    browser ->> auth0-ui: HTTP POST email address
    auth0-ui ->> ses: use SES API
    ses ->> user: send one time code by email
    auth0-ui -->> browser: redirect to code entry screen
    browser ->> auth0-ui: HTTP GET
    auth0-ui -->> browser: code entry screen
    browser -->> user: display code entry screen

    user ->> browser: provide one time code
    browser ->> auth0-ui: HTTP POST one time code
    auth0-ui -->> browser: redirect to auth0/authorize/resume
    browser ->> auth0: GET /authorize/resume
    auth0 -->> browser: redirect to GOV.UK Forms with authorization code

    browser ->> forms: HTTP GET with authorization code
    forms ->> auth0: HTTP POST token request with authorization code
    auth0 -->> forms: ID token, Access token
    forms ->> auth0: Get JSON Web Key Set (JWKS) to verify tokens
    auth0 -->> forms: Respond with JWK file
    forms ->> forms: Verify tokens
    forms ->> forms: extract email address from ID token
    alt First time user has accessed GOV.UK Forms
        forms ->> forms: create record for user
    else Returning user
        forms ->> forms: get record of user
    end
    forms -->> browser: redirect to original requested URL: '/', add user id and current time to _forms_admin_session cookie
    browser ->> forms: Get '/'
    forms -->> browser: Forms homepage HTML
    browser -->> user: display GOV.UK Forms

    note right of user: user is now authenticated
```
