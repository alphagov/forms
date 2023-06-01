# Editing from preview v1

## Status

Date created: *2023-06-01*  

In development  

Development cards:

- [X] [Change preview link to open in current tab/window](https://trello.com/c/Scetz4bk/772-change-preview-link-to-open-in-current-tab-window)  
- [X] [Add “Edit this question” link to DRAFT PREVIEW phase banner](https://trello.com/c/hshsCfY6/777-add-edit-this-question-link-to-draft-preview-phase-banner)  
- [ ] [Spike: investigate how we get users back into the preview journey after making edits to a question](https://trello.com/c/AlwhRECx/780-spike-investigate-how-we-get-users-back-into-the-preview-journey-after-making-edits-to-a-question)    

___

## Contents

- [Status](#status)
- [Contents](#contents)
- [What](#what)
- [Key decisions](#key-decisions)
- [Designs](#designs)
  - [Breaking changes errors](#breaking-changes-errors)
  - [Edit answer type warning](#edit-answer-type-warning)
  - [Notes](#notes)
- [Research focus](#research-focus)

___

<br>

## What

### As-is

- currently we take users to a new tab to preview their form as a form filler would see it  
- there is a “DRAFT” watermark on the background of these screens, which we hope will help form creators keep the “creation” mindset (hat)  
- there is no easy way for users to get back to the edit pages  
- in rounds of research the new tab caused issues and users tried to click the back button to edit pages, with some being lost and needing prompting from the researcher  
- some users suggested being able to quickly edit pages they were on when they saw an issue or error, like a typo or incorrect input type  

### To-be

- form creator creates their questions and can preview their form in “DRAFT” as a form filler would see it  
- preview is now in the same window/tab as the main form creation journey  
- there is a clear way for the form creator to edit the current question page they are viewing  
- there is an easy way to get back to previewing their form where they left off  

## Key decisions

- a tandem piece of work was picked up to [Add a way to show users whether they're looking at a live form, a preview of a live form or a preview of a draft form in the runner](https://trello.com/c/CYcJlAqv/739-add-a-way-to-show-users-whether-theyre-looking-at-a-live-form-a-preview-of-a-live-form-or-a-preview-of-a-draft-form-in-the-runne)
- without the work of the above card, we could start changing the current preview link journey but would not move any further
- we agreed to make the smallest amount of changes to the form builder, improving as we go
- work would be chunked into smaller steps and implemented around larger feature work
  - we had to make sure any step was self contained and would have a minimal overall impact without any dependencies
  - each step should be done in a specific order, but some could be missed or visited in isolation
- larger steps of work would need to be spiked and considered from a technical point of view
- we would not test any of the functionality as a stand alone round of research and instead take findings from other rounds, when and if issues or opportunities came up

<br>

## Designs

### Step 1 of the to-be for draft and live preview

![Step one of the to be draft and live preview screen flow view of a user landing on the “Add and edit your questions” and pressing the “Preview this form” link before being taken to the first screen in the journey, now within the same window or tab. Screenshot of screens from Mural](https://github.com/alphagov/forms/assets/35372982/c10e2578-bb66-4a7e-aaee-aa045a41b7f6)
*caption1*

<br>

### Notes

> Notes to go here.

___

<br>

## Research focus

> No current research has been planned.

<br>

___

<br>

[Back to the top](#editing-from-preview-v1)
