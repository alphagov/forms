# Filling in a form

```mermaid 
sequenceDiagram
  actor user as Form filler
  participant browser as Web Browser
  participant govuk as GOV.UK website
  participant runner as forms-runner
  participant admin as forms-admin
  participant inbox as shared email inbox
  actor processor as Form processor

  user->>browser: Visit GOV.UK page<br />that links to the form
  browser->>govuk: GET
  govuk-->>browser: Show page

  user->>browser: Click link to form
  browser->>runner: GET /form/{form id}/{form slug}
  note over browser,runner: Start 
  runner->>admin: GET /api/v2/forms/{form id}/live
  runner->>runner: determine start page  
  runner-->>browser: 302
  browser->>runner: GET /form/{form id}/{form slug}/{start page id}
  runner->>admin: GET /api/v2/forms/{form id}/live
  browser-->>user: show form

  loop for each form question
    user->>browser: Provide answer, click "Continue"
    browser->>runner: POST /form/{form id}/{form slug}/{page id}
    runner->>admin: GET /api/v2/forms/{form id}/live
    runner->>runner: Save user session
    runner-->>browser: 302
    browser->>runner: GET /form/{form id}/{form slug}/{next page id}
    runner->>admin: GET /api/v2/forms/{form id}/live
    browser-->>user: Show next question    
  end

  browser->>runner: GET /form/{form id}/{form slug}/check_your_answers
  browser-->>user: Show check your answers page
  user->>browser: Click "Submit"
  browser->>runner: POST /form/{form id}/{form slug}/submit-answers
  runner->>admin: GET /api/v2/forms/{form id}/live
  runner->>runner: save Submission
  runner->>runner: enqueue send submission job
  runner-->>browser: 302
  browser->>runner: GET /form/{form id}/{form slug}/submitted
  runner->>admin: GET /api/v2/forms/{form id}/live
  browser-->>user: Show confirmation page
  runner->>inbox: Send email
  inbox->>processor: Read email
```

## Session management


```mermaid 
sequenceDiagram
  %%{init:{"sequence": { "showSequenceNumbers": true }}}%%
  actor user as Form filler
  participant browser as Web Browser
  participant runner as forms-runner
  participant admin as forms-admin

  user->>browser: Click link to form
  browser->>runner: GET /form/{form id}/{form slug}
  runner->>admin: GET /api/v2/forms/{form id}/live
  runner-->browser: REDIRECT 302 (includes first page id)
  browser->>runner: GET /form/{form id}/{forms slug}/{page id}
  Note over browser,runner: A new session has started 
  browser-->>user: show "form start page"
  loop every question of the form
    user-->browser: Fills in the answer to question<br>clicks "Continue" button
  end
```

## Brief summary

The users answers are store in Redis in the following structure as they progress through the form.

```
{
   "answers": {
    "{form id}": {
      "{page id}": {
        ... input field names and their answers...
      },
      "{page id}": {
        ... input field names and their answers...
      },
      ... for each page/question that the users answers
    },
    ... above repeated for each form a users is completing
  }
}
```

The Redis session's TTL is set to 20 hours, the expiry time resets after each request a user makes to
`forms-runner`. 

### Example of Redis session

#### Scenario: 

Two existing forms, Form 1 (id=11), Form 2 (id=22). 
Form 1 has 2 pages, Form 2 has 1 page.

When the user visits the service for the first time but has not answered any questions. 

```
{
  "answers": {},
  "_csrf_token": "blahblahblahblahblah"
}
```

Once a user answers the first question, the form id (In this case Form 1) is recorded as a key and another object with the page id is created along with the fields and answers for that page type. In this case the page id is "1" and it is a name answer type.

```
{
  "answers": {
    "11": {
      "1": {
        "title": null,
        "full_name": "Al",
        "first_name": null,
        "middle_names": null,
        "last_name": null
      }
    }
  },
  "_csrf_token": "blahblahblahblahblah"
}
```

They progress to question 2 of Form 1 and answer that. Again it would be page id "2" and it is a date answer type.

```
{
  "answers": {
    "11": {
      "1": {
        "title": null,
        "full_name": "Al",
        "first_name": null,
        "middle_names": null,
        "last_name": null
      },
      "2": {
        "date_day": "1",
        "date_month": "2",
        "date_year": "2023",
        "date": "2023-02-01"
      }
    }
  },
  "_csrf_token": "blahblahblahblahblah"
}
```

Before submitting the answers for Form 1, the user decides (for whatever reason) to start completing Form 2. Nothing changes when they appear on the first question of the form. Once they have filled in the fields and press "Continue", the form id & page id etc are added to the same redis session.

```
{
  "answers": {
    "11": {
      "1": {
        "title": null,
        "full_name": "Al",
        "first_name": null,
        "middle_names": null,
        "last_name": null
      },
      "2": {
        "date_day": "1",
        "date_month": "2",
        "date_year": "2023",
        "date": "2023-02-01"
      }
    },
    "22": {
      "3": {
        "number": "42"
      }
    }
  },
  "_csrf_token": "blahblahblahblahblah"
}
```

They continue on with Form 2 and submit their answers. The value for Form 2 key (id=22), is set to null but Form 1 answers still persist. 

```
{
  "answers": {
    "11": {
      "1": {
        "title": null,
        "full_name": "Al",
        "first_name": null,
        "middle_names": null,
        "last_name": null
      },
      "2": {
        "date_day": "1",
        "date_month": "2",
        "date_year": "2023",
        "date": "2023-02-01"
      }
    },
    "22": null
  },
  "_csrf_token": "blahblahblahblahblah"
}
```

The user ends up going back to the Form 1 to submit their answers which again sets that form key value to null.

```
{
  "answers":{
    "1":null,
    "2":null
  },
  "_csrf_token": "blahblahblahblahblah"
}
```

#### Expiry

The expiry time resets every time the user refreshed/submits the page (i.e shows some activity happen). The session will also end if the user closes their browser. The CSRF token value does not make the cookie value in the browser but Rails must keep a record of which cookie value related to which particular redis session record.