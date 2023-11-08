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
    browser ->> forms: HTTP GET
    forms ->> forms: no session cookie found
    note right of forms: using Auth0 OmniAuth strategy
    forms -->> browser: redirect to authenticate
    browser ->> auth0: HTTP GET
    auth0 -->> browser: login screen
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
    forms ->> forms: create user session
    forms -->> browser: set session cookie
    browser ->> browser: store session cookie
    browser -->> user: display GOV.UK Forms

    note right of user: user is now authenticated

```
