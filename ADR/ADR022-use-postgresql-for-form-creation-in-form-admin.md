# ADR022: Store forms in forms-admin before sending to forms-api

Date: 2023-09-14

## Status

> Accepted

## Context

See https://app.mural.co/t/gaap0347/m/gaap0347/1695033470183/a0f2dd9bdd9b698b1a411c8bfbcc33a9e5f987b0?sender=10492031-8763-46d6-ab0b-b41eb037cc4e

Originally forms-admin didn't have a workflow but a single screen for the user to draft their form. This got broken up into a multistage workflow. Data is transferred between screens via cookies but this has limitations, and only worked ok for a linear flow. Now that we are approaching diverging workflows, we can't support this any longer. We are also currently only using ActiveModel for our classes.

Users configure `pages` in forms admin over multiple steps (sometimes called a wizard 🧙!). `Pages` are only saved in a form when a user has completed all the required steps. Different answer types have difference steps.

For example, the user chooses the "date" answer type, then on the following screen selects that it will be a date of birth and on the last screen enters the question text. The user then saves the `page`, at which point the `page` is added to the `form`.

Currently we use the [form object pattern](https://dev.to/drbragg/rails-design-patterns-form-object-4d47#:~:text=Form%20Object%20Pattern,consistent%20API%20in%20our%20code.) to manage the intermediate state of pages as they are being created.

 This gives each screen a [model](https://github.com/alphagov/forms-admin/tree/main/app/forms/pages), [controller](https://github.com/alphagov/forms-admin/tree/main/app/controllers/pages) and [view](https://github.com/alphagov/forms-admin/tree/main/app/views/pages).

We store the state of incomplete `pages` in the session hash. The code updating this hash is spread across the form objects and controllers. When adding or modifying steps in the `page` journey, it's up to the programmer to make sure the session is updated correctly, such as making sure it's cleared in the right places.

As we've added more features for `pages` such as extra input types, conditions and additional guidance, managing state in the session hash has become harder. We've had issues around producing inconsistent data, using a mix of strings and symbols and deleting data at the wrong point.

Also, as the session hash is currently stored in user's cookie, there is a size limit of 4kb. This is not an immediate issue but could pose difficulties when a `page` has many question options, long guidance text or we start using the session in other parts of the application.

## Strategy

We should:

This ADR proposes that we stop using the forms object pattern to create pages. Instead each step is represented using an activeRecord model and database table. This means we no longer need to use the session hash to maintain the state of incomplete pages, removing the burden to manage it from the programmer. In essence we are moving from the "hard way" to the "easy way" in this [breakdown of multi-page forms](https://www.codewithjason.com/rails-multi-step-forms/). When a user finished configuring a `page` the different records would be collected together and submitted to the API as before.

Essentially:

* Refactor our models to be more Rails-standard and switch from ActiveModel (doesn't easily persist locally) to using ActiveRecord (allows us to easily persist locally) on our classes.

* Rather than manually managing data in session for the user, as the user takes an action the data entered via the form is persisted to the PostgreSQL database for forms-admin.

* Use the PostgreSQL database to manage data.

* Drop using cookies for data in session (other than checking if the user is logged in)

## Decision

* We add a new class that is an ActiveRecord model. This is a join table between Forms and Pages in the database.
* Temporarily, we keep use of `FormObjects` to break up the record into multiple pages and validate at those steps, before saving the record.

## Consequences

### Pros

* removes need for Redis instance
* it makes the app more standard Rails
* it removes massive tech debt (where we went from a single-page, zero workflow interface to trying to adapt it to have some workflow)
* it makes things easier to implement
* it’s easier to validate
* data is more stable
* users don’t lose their data as their workflow diverges
* as more complexity is added to the workflow, we won’t be adding to that tech debt and working against and increasing brittleness
* developers don't need to manage incomplete page state "by hand" as we could fallback on active record to save records to the database. This matches how we manage other parts of the form.
* less likely for data to be deleted accidentally.
* lets us delete some existing session handling code and tests.

### Cons

* Risk of duplication of business logic between api and admin apps. This is why the concern of the api is to act as the "single source of truth" for forms, and only be concerned with rendering *viewable* forms, both previews and live.
