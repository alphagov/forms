# ADR014: Add conditions table to the database

Date: 2023-02-28

## Status

Accepted

## Context

In order to implement the simple routing work, we need to store conditions in our database. A condition is a data structure that needs to contain information about how the runner should calculate whether a user should be skipped forward to a certain page in the form, based on their answers to previous questions. For the simple routing information, the IDs for the question being checked, the question where the routing takes place, and the destination question in the case of the condition being met all need to be stored. Additionally, the matching answer to the question being checked also needs to be included. An example of a JSON object condition would look like this.

```
{
  "prior_question_id": 1,
  "current_question_id": 2,
  "goto_question_id": 4,
  "answer_value": "Yes",
}
```

We have different options for how we store this information, either as a field on the Page table, or in a separate Conditions table. 

## Decision

The team has decided to go with the option of a new Conditions table, which will be associated with Pages. Pages will be able to have multiple conditions, each of which will be represented by a new row in the Conditions table. 

## Consequences

Storing conditions as a separate table will allow us to utilise Rails' relational ActiveRecord tools more easily. This means that identifying any and all conditions associated with a given Page will be easy, and will make checking for logical routing errors and alternative routing paths simpler. 

However, if in the future we decide to introduce more complex types of conditions, we may find ourselves slightly constrained by having conditions stored in a table, as opposed to a more freeform JSON object. We may need to introduce a variety of columns to account for different sorts of conditions. 
