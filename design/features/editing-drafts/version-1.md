# Editing draft forms from preview: v1

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

- Currently, we take users to a new tab to preview their form as a form filler would see it  
- There's a “DRAFT” watermark on the background of these screens, which we hope will help form creators to retain the 'creation' mindset (or 'hat')  
- There's no easy way for users to get back to the edit screen of whichever question they're previewing  
- During research the new tab caused issues as users tried to click the back button to edit the page they were viewing: some got lost and needed a prompt from the researcher  
- Some users said they'd like to be able to quickly edit the pages they were on when they spotted an issue or error, like a typo or incorrect input type 

#### Current design for preview screens 

The following designs were developed alongside the work to help users easily identify which version of the form they were looking at. At the same time, the Forms team were developing the new feature that allows a new draft form to be created from an existing live form without making the changes instantly live.

![Draft preview with updated phase banner using “DRAFT PREVIEW” purple tag next to content that says “You're previewing the draft version of this form”. The word “DRAFT” appears at an angle and is repeated across the screen, from left to right and top to bottom. Screenshot of Mural board design](https://github.com/alphagov/forms/assets/35372982/5898c1fe-77b7-4130-876b-cb8136d5a07b)

![Live preview with updated phase banner using “LIVE PREVIEW” blue tag next to content that says “You're previewing a live form”. The word “PREVIEW” appears at an angle and is repeated across the screen, from left to right and top to bottom. Screenshot of Mural board design](https://github.com/alphagov/forms/assets/35372982/49f0242a-ded3-44b0-9b18-8991e48d716a)

<br>

### To-be

- Form creator creates their questions and can preview their form in “DRAFT” as a form filler would see it  
- Preview now opens in the same window/tab as the main form creation journey  
- There's a clear way for form creators to edit the question page that they're currently viewing  
- There's an easy way for form creators to get back to previewing their form from where they left off  

## Key decisions

- Another piece of work was picked up at the same time to [Add a way to show users whether they're looking at a live form, a preview of a live form or a preview of a draft form in the runner](https://trello.com/c/CYcJlAqv/739-add-a-way-to-show-users-whether-theyre-looking-at-a-live-form-a-preview-of-a-live-form-or-a-preview-of-a-draft-form-in-the-runne)
- Without the work on the above card, we'd have been able to start changing the current preview link journey but we would not have been able to take it much further
- We agreed to make the smallest number of changes to the form builder possible, improving on this as we go
- Work would be chunked into smaller steps and implemented around larger feature work
  - We had to make sure that any one step was self contained and would have minimal overall impact with no dependencies
  - Each step should be done in a specific order, but some could be missed or visited in isolation
- Larger steps of work would need to be spiked and considered from a technical point of view
- We would not test any of the functionality as a standalone round of research but would instead use findings from other research rounds if and when issues or opportunities came up

<br>

## Designs

Mural board:  
https://app.mural.co/t/gaap0347/m/gaap0347/1679397321141/0240133a9118f567e73363eb32bd7136454d31e0?wid=0-1680685000213

### Step 1 of the 'to-be' for draft and live preview

![Step 1 of the 'to-be' draft and live preview screen-flow view for a user landing on the “Add and edit your questions” page and pressing the “Preview this form” link before being taken to the first screen in the journey, which is now within the same window or tab. Screenshot of screens from Mural](https://github.com/alphagov/forms/assets/35372982/c10e2578-bb66-4a7e-aaee-aa045a41b7f6)

As part of step 1 we'll keep the user in the same window or tab, which:
- will help users use the back button to navigate back to make changes and fixes
- is a mental model we saw in research

There should be no change to the banner across Draft / Live preview.

<br>

### Step 3 of the 'to-be' logged-in draft preview

![Step 3 of the 'to-be' draft preview: screen-flow view of a logged-in user previewing their form. The draft preview now has a new phase banner and content with a quick link to edit the page they're currently previewing. Screenshot of screens from Mural](https://github.com/alphagov/forms/assets/35372982/015bf848-114c-427e-95c5-70e356550cfa)

As part of step 3:
- we'll add an edit link to the banner. Anchor text will say “Edit this question” and will take the user to the “Edit question” screen for the question they're currently previewing
- after editing the question, the user can either:
  - “Save question”, which reloads the “Edit question” screen (as normal behaviour)
  - “Save and [add/edit] next question”, continuing with current behaviour

<br>

### Notes

- Delete button will work as normal with an interim “Are you sure?” page before returning the user to the:
  - question list page if they select “Yes”
  - “Edit question” page if they select “No”
- Back link should take the user to the question list page  
Note: users can still use the browser's back button, which will take them back to the page they left in the journey. This means they could make changes and go back into the preview journey where they left off without experiencing any issues (though they'll need to refresh the screen to see their changes)
- We've removed the grey “Save question” button - to be revisited when we look at previewing a question while creating it (static unlinked version)

<br>

As part of step 4 we'll explore the save button becoming “Save and continue”, which would return the user to the question list page.

<br>

As part of step 5 we'll look at returning the user to the question they’ve edited after they save changes using either a:
- “Save and preview” grey button 
- link to get them back into the journey

This will need to be discussed and prioritised.

<br>

![Step 3 of the 'to-be' screen-flow view of a logged-in user previewing their “Live” form. Left shows a “Go to your form” link in the banner because a “Draft” version of the current form exists. This links the user to the static “Live” form view, where they can edit or create a draft. Right shows a “Create draft version of this form” link in the banner and links the user to the “Create a form” screen with a new “Draft” state version of their form showing all the tasks marked as “COMPLETED”. Screenshot of screens from Mural](https://github.com/alphagov/forms/assets/35372982/619ca8bf-a749-4369-9bef-84845ec72410)

We also discussed a way to check if a user is signed into the form builder, and only showing the link to edit the page when logged in. This would be replicated on Live previews, but would take the user to create a new draft of the form where a draft did not exist.  

This is complex behaviour and may be considered at a later date if it’s seen as being a justified need at that point.

___

<br>

## Research focus

No research is currently planned.

<br>

___

<br>

[Back to the top](#editing-from-preview-v1)
