# Features

Intro about features and that features described here relate to the ones we have designed and developed into the product directly, rather than the prototype.

We can include main names of the features and iterations.

## Live and draft feature

### Problem we tried to solve

- GOV.UK Forms had no way of making safe changes to a live form, without disrupting end users. This was a [decision made](https://github.com/alphagov/forms/blob/main/decision-record/DR007-form-is-live-first-then-add-draft.MD) to enable GOV.UK Forms to make first form live 
- Form creators were interrupted and warned about making changes to a live form before and after making their form live
- When form creators made changes to live forms the changes were applied immediately and could break experience for end users while mid way through using a form
- We didn't support changes to go live at a certain date
- Form creators didn't have a way to prepare edits, and have a form reviewed before making changes live

### User needs

- As a form creator, I need to make changes to a form that went live, so that the latest form can be available to users
- As a form creator, I need to make changes in a safe way, so that our end users experience of forms is not disturbed

### Hypothesis

- We think that if we provide a way to make edits of a live form within a draft copy of it, then form creators can safely make their changes without affecting the live form and disrupting end users
- We think that if a form creator has completed their updates in a draft state, then they will be able to replace the 'old' live form with a new version of a form in a live state

### What we did

- We ran a series of team activities to ideate and refine what the new journey would look like for form creators to make changes in a draft state.
- We wireframed and made multiple iterations of the design and user journey and then we began implementing the designs into the GOV.UK Forms product under a feature flag
- We have tested the new feature with a group of users and [collated insights](https://docs.google.com/document/d/1FJnES5zJoL6-kYUMmdKOUBcfWi6caYfrCdnL7iypzw4/edit?usp=sharing)

### Outcome

- [First tested iteration of making changes to a live form feature](/design/features/live-draft/version-1.md)
- We created an improved user journey of making changes to a live form in a draft state
- We added new view only pages to present information about a form in a live state, like questions
- We added a modified task list page for editing a form in a draft state
- We have iterated form preview pages to clearly distinguish draft previews from live previews in an accessible way
- During usability sessions users were able to successfully make changes to a form in a draft state and understood the concept
- From research sessions we have learned about areas for improvement to iterate on further