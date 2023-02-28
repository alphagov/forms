# ADR013: Add conditions to page model

Date: 2023-02-28

## Status

Accepted

## Context

### Option 1

Questions either have a next page when they're unconditional, or a set of conditions if there need to be conditional routing checks. This is not as preferable as the second option, as it requires us to construct more of a branching system whereby all outputs to a conditional question are specified - so all routes out of that question are covered by conditions. The user will implicitly set up routes in different directions, and we'd have to calculate them explicitly.

There's potentially a bit of value down the line in being extremely explicit about all the ways a route resolves, but it's kind of hard to think about them now.

#### api

```json
{
  "id": 1,
  "next_page": 2,
  "conditions": null
}
```

```json
{
  "id": 1,
  "next_page": null,
  "conditions": [
    { "question_id": 1, "match_answer": "first option", "destination_id": 3 },
    { "question_id": 1, "match_answer": "second option", "destination_id": 2 }
  ]
}
```

#### runner

```ruby
def calculate_next_page(page)
  unless page.next_page.nil?
    return page.next_page
  end

  page.conditions.each do |condition|
    given_answer = session[condition.question_id].answer
    return condition.destination_id if given_answer == condition.match_answer
  end
end
```

### Option 2

Alternatively, question pages will always have a default `next_page` which can be deferred to - but if they have any `conditions`, those will be checked against primarily and take precedence over the `next_page` if any are met. This is what I prefer, as it lets us make minimal additions to questions.

#### api

```json
{
  "id": 1,
  "next_page": 2,
  "conditions": [
    { "question_id": 1, "match_answer": "first option", "destination_id": 3 }
  ]
}
```

#### runner

```ruby
def calculate_next_page(page)
  page.conditions.each do |condition|
    given_answer = session[condition.question_id].answer
    return condition.destination_id if given_answer == condition.match_answer
  end

  return page.next_page
end
```

I have a slight concern here that conditions will be captured the "wrong way around" - the default page will always be the one that's next in the position, but the routing will need to display this as the condition, rather than the default e.g.

```
frontend:
Question 1
  Question text: Do you have a name?
  Option 1: Yes
  Option 2: No

Question 1 Condition
  If: "Do you have a name?"
  Answered with: "Yes"
  Goto: 3
```

In the backend this would look alright, as the condition attached to the question would be `{question_id: 1, match_answer: "Yes", destination_id: 3}`. you know what nevermind!

### Option 3

The `next_page` field could simply be the single source of information for where to calculate the next page. This has the advantage of making it straightforward to identify what the next page should be from a single field. The main issue would be the possibility of overcomplicating a single field, as it would potentially have to store quite a wide range of data (as it would need to effectively implement one of the two previous options _within_ the `next_page` field)

#### api

```json
{
  "id": 1,
  "next_page": { "default": 2, "conditions": [] }
}
```

```json
{
  "id": 1,
  "next_page": {
    "default": 2,
    "conditions": [
      { "question_id": 1, "match_answer": "first option", "destination_id": 3 }
    ]
  }
}
```

This does turn next page into a good place to store all the information about where the runner should take the user

#### runner

The runner could implement a method in the page model that works out the next page in context.

This way, page objects can have their `next_page` queried, which can return the id for the next page.

```ruby
  def next_page
    next_page.conditions.each do |condition|
      given_answer = session[condition.question_id].answer
      return condition.destination_id if given_answer == condition.match_answer
    end

    return next_page.default
  end
```

### Option 4

I'm not a fan of this, I think routing should be connected to the question now. I used to think it would be good to have clear branch points which weren't attached to specific questions, but I don't think this is the simplest way of doing that.

I would prefer if we connect `conditions` to a `page`, whether that's a question page or some other kind of page (information page, start page etc.) rather than having a separate page.

It make sense that pages represent things that are shown to a form filler, and could be mapped across to a page being displayed - routes are not this, and represent more of a meta-structure thingy.

#### api

```jsonc
/* Question page */
{
  "id": 1,
  "page_type": "question",
  "next_page": 2,
  "question_text": "...",
},

/* Routing page */
{
  "id": 2,
  "page_type": "route",
  "conditions": [
    {"question_id": 1, "match_answer": "first option", "destination_id": 3},
    {"question_id": 1, "match_answer": "second option", "destination_id": 4},
  ],
}
```

#### runner

pretty messy, would need to detect what sort of page the next page was, and if it's a `route` page do the same thing again (recursively until you get an actual page number)

would take a bit more work to get it working

I think the benefit here is that you can make very articulate `condition` page types, that don't have to fit inside the `question` page type format.

These are also decoupled from question pages, which lets thing move around a bit more easily if you're reordering things

```ruby
def calculate_next_page(page)
  if page.page_type == "question"
    return page.next_page
  end

  if page.page_type == "route"
    page.conditions.each do |condition|
    given_answer = session[condition.question_id].answer
    return condition.destination_id if given_answer == condition.match_answer
  end
end
```

I think the only redeeming feature here is that it suits the admin side a bit more, as routes become their own thing rather than tethered to questions, but so far the design doesn't require this. It also doesn't look like it'd be _that_ hard to migrate existing conditions into their own separate route pages if we absolutely had to - all they have is three bits of data for each condition.g

### More considerations

#### Overlapping conditions

For simple routing, we're only going to attach a single condition to each question at most. This means that we won't get priority problems with multiple conditions depending on which one triggers first e.g. a question that reroutes based on several prior questions, where the user's answers could divert them off on all kinds of paths.

However, in the future we might start to get more complex routes, where a user's answers to several questions are all potential condition triggers, and one of them should be taking priority e.g.

```
Question 1: Do you have a pet?
  Option 1: Yes
  Option 2: No

Question 2: What colour is your car?
  Option 1: Red
  Option 2: Yellow
  Option 3: None of the above

Conditional route:
  Question: What colour is your car?
  Answer match: Yellow
  Goto: 4

Conditional route:
  Question: Do you have a pet?
  Answer match: Yes
  Goto: 3

Question 3: What's your name

Question 4: How old are you
etc.
```

In this example, the order of the conditions will potentially determine whether a user sees question 3, and communicating to the admin-user how their overlapping conditions function will be a challenge. For now we don't have to worry too much, but it would be good to think about this in terms of structuring the data in a way that doesn't make this a pain to refactor. It would probably be healthy anyway to design it more nicer

#### Other page types

We've currently only got question pages, but we deliberately left possibility open for other page types. I think something like a kickout or payment page was what was in mind at the time, but routing is a possibility for a more meta page, as it still fits in the sequencing of a form nicely. If we attach it to questions, then it makes moving routes around a bit more painful, and something we should ask design team

#### Well formed Forms

As part of the admin form builder, we need to show error messaging whenever a form and its routes are in an unworkable state. For example, if I move a question above a condition that gotos it, then we need to be able to calculate the error. It's worth thinking about how we would do this using the data structure we end up with. Here's some starter points

- We'd check over each question, and see if they have conditions
- If they do, we'd want to check that the checked question occurs before the routing
- And that the answer match is a possible selection option in the list
- and that the destination id occurs later in the page order sequence
- but that the destination id doesn't occur immediately in the page order sequence, otherwise the route is trivial

Are there any other logic slaps we should/could to do?

#### Sections, branches, visualisation etc.

There's potentially a lot of upcoming stuff around routing that we haven't got full designs for (intentionally), but if there's anything that immediately sticks out as irreconcilable it'd be good to draw attention to it

## Decision

The team has opted to go with option 2.

## Consequences

> both positive and negative consequences of the decision
