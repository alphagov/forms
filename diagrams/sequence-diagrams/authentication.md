## Accessing GOV.UK Forms via Auth0

```mermaid
sequenceDiagram
    autonumber
    title Accessing GOV.UK Forms via Auth0
    actor user as unauthenticated user
    participant browser as web browser
    participant forms as GOV.UK Forms
    participant auth0 as Auth0
    participant ses as Amazon SES

    user ->> browser: visit GOV.UK Forms
    browser ->> forms: HTTP GET /
    forms ->> forms: no _forms_admin_session cookie from client, cookie does not contain user_id or the auth_timestamp is older than 24 hours
    note right of forms: using Auth0 OmniAuth strategy
    forms -->> browser: redirect to /auth/auth0, set _forms_admin_session cookie
    browser ->> forms: HTTP GET /auth/auth0
    forms -->> browser: redirect to /authorize
    browser ->> auth0: HTTP GET /authorize
    auth0 -->> browser: redirect to Universal login
    browser ->> auth0: GET /u/login/
    auth0 -->> browser: Login page
    browser -->> user: display login screen

    user ->> browser: provide email address
    browser ->> auth0: HTTP POST email address
    auth0 ->> ses: use SES API
    ses ->> user: send one time code by email
    auth0 -->> browser: redirect to code entry screen
    browser ->> auth0: HTTP GET
    auth0 -->> browser: code entry screen
    browser -->> user: display code entry screen

    user ->> browser: provide one time code
    browser ->> auth0: HTTP POST one time code
    auth0 -->> browser: redirect to auth0/authorize/resume
    browser ->> auth0: GET /authorize/resume
    auth0 -->> browser: redirect to GOV.UK Forms with authorization code

    browser ->> forms: HTTP GET with authorization code
    forms ->> auth0: HTTP POST token request with authorization code
    auth0 -->> forms: ID token, Access token
    forms ->> auth0: GET JSON Web Key Set (JWKS) to verify tokens
    auth0 -->> forms: Respond with JWK file
    forms ->> forms: Verify tokens
    forms ->> forms: extract email address from ID token
    alt First time user has accessed GOV.UK Forms
        forms ->> forms: create record for user
    else Returning user
        forms ->> forms: GET record of user
    end
    forms -->> browser: redirect to original requested URL: '/', add user id and current time to _forms_admin_session cookie
    browser ->> forms: GET '/'
    forms -->> browser: Forms homepage HTML
    browser -->> user: display GOV.UK Forms

    note right of user: user is now authenticated
```
