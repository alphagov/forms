## Live and draft
The ability to make a draft of a live form to prepare changes to it. You can then make all the changes live at the same time, and at an appropriate time.

### Problems we tried to solve

- GOV.UK Forms had no way of making safe changes to a live form, without lots of disruption for end users. This was a [decision made](https://github.com/alphagov/forms/blob/main/decision-record/DR007-form-is-live-first-then-add-draft.MD) to enable GOV.UK Forms to make the first form live 
- When form creators made a change to a live form each change was applied immediately - each time this could affect anyone who might be filling in the live form at the time
- There was no way to make a group of changes all live at a certain date or time
- Form creators didn't have a way to prepare a group of changes that could be shared and reviewed before making them live
- Form creators were warned about the potential impacts of making a change to a live form before and after making their form live

### User needs

- As a form creator, I need to make changes to a form that is live, so that the latest form can be available to users
- As a form creator, I need to make changes in a safe way, so that our end users experience of forms is not disturbed

### Hypothesis

- We think that if we provide a way to make edits of a live form within a draft copy of it, then form creators can safely prepare their changes without affecting the live form and disrupting end users
- We think that if a form creator has completed their updates in a draft state, then they will be able to replace the 'old' live form with a new version of a form in a live state, minimising disruption to end users

### What we did

- We ran a series of team activities to ideate and refine what the new journey would look like for form creators to make changes in a draft state.
- We wireframed and made multiple iterations of the design and user journey and then we began implementing the designs into the GOV.UK Forms product under a feature flag
- We have tested the new feature with a group of users and [collated insights](https://docs.google.com/document/d/1FJnES5zJoL6-kYUMmdKOUBcfWi6caYfrCdnL7iypzw4/edit?usp=sharing)

### Outcome

- [The first tested iteration of making changes to a live form](/design/features/live-draft/version-1.md)
- We created an improved user journey of making changes to a live form in a draft state
- We added new view only pages to present information about a form in a live state, like its questions
- We added a modified task list page for editing a form in a draft state
- We have iterated form preview pages to clearly distinguish draft form previews from live form previews in an accessible way
- During usability sessions, users were able to successfully make changes to a form in a draft state and understood the concept
- From research sessions we have learned about areas for improvement to iterate on further
