# ADR008: Page ordering defined by pointers to the next page in form objects

Date: 2022-05-31

## Status

> Proposed

## Context

When the forms runner is reading forms - it needs to be aware of the ordering of pages and how to navigate from one page to the other.

During private beta we're only considering forms which have no branching paths, however we know this is a future requirement and want to consider how any solution we choose may get extended in the future to support branching.

### Option one: Return pages in an array and progress to the next page based on array position

```json
{
  "pages": [
    {
      "id": "first-page"
    },
    {
      "id": "second-page"
    }
  ]
}
```

### Option two: Give pages an "position" value, progress based on the next position value

```json
{
  "pages": [
    {
      "id": "second-page",
      "position": 2
    },
    {
      "id": "first-page",
      "position": 1

    }
  ]
}
```

### Option three: Treat pages as a linked list, with a pointer to the next page

```json
{
  "pages": [
    {
      "id": "second-page",
      "next": "final-page"
    },
    {
      "id": "first-page",
      "next": "second-page"
    },
    {
      "id": "final-page"
    }
  ]
}
```

This takes inspiration from the original submit JSON structure:

https://github.com/alphagov/submit-prototype-kit/blob/master/examples/simple.json

----

Of the three options only option 3 gives the ability to extend it in the future for branching purposes as both 1 and 2 are based on a linear ordering whereas 3 gives us the opportunity to expand it in the future, by replacing the string value with an object which can provide the rules for branching.

## Decision

The team has opted to go with option 3.

## Consequences

- We will be able to navigate from one page to the next
- Navigating backwards will be more challenging as we don't have a pointer backwards
- We will be able to support branching in the future
