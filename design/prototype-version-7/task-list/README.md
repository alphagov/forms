# Create a form (task list page) page

## Context

We tested version 6 of the task list page in usability testing sessions with form creators who had form builing experience and some with low digital confidence. 

We tested the design of the page, checking users understanding of the process to get a form live and how they navigate through the tasks. 

This provided us with some valuable insights and formed the basis of version 7. 

## What we tested last time

![Create a form task list page. Screenshot](https://github.com/alphagov/forms/blob/main/design/prototype-version-6/screenshots/003-Create-a-form-Apply-for-a-juggling-licence.png)
*Page with “Apply for a juggling licence” caption above the heading that says “Create a form”.*

Below the heading is bold text saying “Form incomplete“ that tells the form creator they have not completed all the steps to create their form. There is a parapgrah text next saying “You have completed 1 of 10 sections.“ This tells the form creator how many sections out of the total sections they have completed. 

There is a table with the first set of tasks that a form creator needs to complete to create a form, with the caption “1. Create your form“

The first row has a link to “Edit the name of your form“ and a blue highlighted tag on the far right of the row that reads “completed“.

The second row has a link to “Add and edit your questions“ and a grey highlighted tag on the far right of the row that reads “not started“.

The third row has a link to “Review summary page and add declaration“ and a grey highlighted tag on the far right of the row that reads “not started“.

The fourth row has a link to “Add information about what happens next“ and a grey highlighted tag on the far right of the row that reads “not started“.

There is a another table with the second set of tasks, with the caption “2. Set form responses“
The first row has a link to “Set the email address completed forms will be sent to“ and a grey highlighted tag on the far right of the row that reads “not started“.
The second row has an inactive link to “Enter the email address confirmation code“ and a grey highlighted tag on the far right of the row that reads “Cannot start yet“. This inactive link changed to an active when the form creator completes the previous step and the grey highlighted status tag would change to “not started“.

Next is another table with the third section of tasks, with the caption “3. Get your form ready to go live“
The first row has a link to “Provide link to your privacy information“ and a grey highlighted tag on the far right of the row that reads “not started“.
The second row has a link to “Provide link to your accessibility statement“ and a grey highlighted tag on the far right of the row that reads “not started“.

Next is a table with the fourth set of tasks, with the caption “4. Publish your form“
The first row has a link to “Make your form live“ and a grey highlighted tag on the far right of the row that reads “not started“.
The second row has a link to “How to publish the form on GOV.UK“ and a grey highlighted tag on the far right of the row that reads “not started“.

Below these is a closed details component showing a blue link with an arrow before the text “Add hint text to help people answer the question”.

### What we saw

- Users found the task list clear, easy to use and logical to navigate
- Users found the progress labels helpful to work through the list and used them regularly.  
- All tasks were successfully completed apart from email setup which was not entirely clear to one low digital confidence user. 
- All users completed the tasks in order, but when questioned said they understood it could be completed in any order.
- The link text to “Review summary page and add declaration“ was not clear to all users. This became clearer for some when they clicked the link to get to the ‘what happens next’ page.
- When users clicked on the link to “Add and edit your questions“ tasks, and added their questions, the grey highlighted tag on the far right of the row changed to a light blue tag that reads “in progress“ as shown below. Users were unsure how to move the tag to “complete“

![Create your form tasks. Screenshot](.../design/prototype-version-6/screenshots/003-1-Task-list-page-tags-focus-create-your-form.png)
*Table with caption “1. Create your form” and four rows with link texts to tasks and tags on the far right of the rows.*

## What we changed and why

- Added a purple highlighted tag labelled “DRAFT“ for when the form is in draft and a green highlighted tag labelled “LIVE“ for when the form has been made live. 
- Changed the link text from “Review summary page and add declaration“ to “Add a declaration for people to agree to“. This made the task and action for the form creator clear.

![Create your form. Screenshot](.../design/prototype-version-7/screenshots/003-create-form-create-form-statuses-focus.png)
*Table captioned “1. Create your form“ and four rows below with link texts and tags on the far right.*

- Changed table caption for the second set of tasks from “2. Set form responses“ to "2. Set email address for completed forms“

![Set email address for completed forms. Screenshot](design/prototype-version-7/screenshots/003-create-form-set-email-statuses-focus.png)
*Table captioned "2. Set email address for completed forms“ and two rows below with link texts and tags on the far right.*

- Changed table caption for the third set of tasks from “3. Get your form ready to go live“ to “3. Provide privacy and contact details“
- Edited the link text for the first task on table from “Provide a link to your privacy information“ to “Provide a link to privacy information for this form
- Changed the link text on second row of the table captioned “3. Provide privacy and contact details“ from “Provide link to your accessibility statement“ to “Provide contact details for support“. This task was introduced so that form creators can provide at least one way for people to get help if they get stuck while filling in their form.
  
![Provide privacy and contact details. Screenshot](design/prototype-version-7/screenshots/003-create-form-privacy-contact-statuses-focus.png)
*Table captioned “3. Provide privacy and contact details“ and two rows below with link texts and tags on the far right.*

- Changed table caption for the fourth set of tasks from “4. Publish your form“ to “4. Make your form live“.
- Removed the final task ““How to publish the form on GOV.UK“ because the guidance to publish a form on GOV.UK was provided in the [“Make your form live“](design/prototype-version-7/screenshots/701-make-your-form-live.png) page.
- Added a red “Delete” button at the bottom of the page.

![Make your form live. Screenshot](https://github.com/alphagov/forms/blob/documenting-prototype-version-7/design/prototype-version-7/screenshots/003-create-form-make-live-focus.png)
*Table captioned “4. Make your form live“ and a row below with an inactive link text and tag on the far right.*

## What we designed for version 7

![create a form task list page. Screenshot](screenshots/003-create-form.png)
*Create a form (task list page) for a draft form with “Apply for a juggling licence” caption above the heading that says “Create a form”. Followed by a purple tag that says “DRAFT“.*
![task list page for a live form. Screenshot](screenshots/703-create-form-live.png)
*Create a form (task list page) for a live formPage with “Apply for a juggling licence” caption above the heading that says “Your form”. Followed by a green “LIVE“ tag.*
