# Prototype version 7

Dates tested: 

## Status

Superceeded by [version 8](../prototype-version-8) -->

___

## Contents

- [Context](#context)
- [Admin interface screenshots](#admin-interface-screenshots)
- [Form runner screenshots](#form-runner-screenshots)
- [What we learned](#what-we-learned)
- [Opportunites](#opportunities)

___

<br>

## Context

> **Sprint X**
> In this sprint we want to test

<br>
<br>

## Admin interface screenshots

Below are the screens a form creator will see when making or editing their forms.

<br>

### GOV.UK Forms landing page

![GOV.UK Forms landing page. Screenshot](screenshots/001-form-home-landing.png)
*Page with “GOV.UK Forms” heading and green “Create a form” start button.*

<br>

### Name your form page

![What is the name of your form question page. Screenshot](screenshots/002-form-create-a-form.png)
*Page with “What is the name of your form?” question heading.*

There is hint text that says, “The form name will be shown at the top of each page of the form. Use a name that describes what the form will help people to do. For example ‘Apply for a juggling licence’.” above a text input.

Below the text input is a green “Save and continue” button.

<br>

### Create a form (task list page)

![Create a form task list page. Screenshot](screenshots/003003-create-form.png)
*Page with “Apply for a juggling licence” caption above the heading that says “Create a form”.*

There is a purple "draft" status tag 

<br>

### Add and edit your questions page

![Add and edit your questions page. Screenshot](screenshots/004-form-index-no-questions.png)
*Page with “Apply for a juggling licence” caption above the heading that says “Add and edit your questions”.*

There is a purple status tag with a descriptor 'draft' to let users know this is a draft form. 
There is a green “Add a question” button.

<br>

### Edit question 1
![edit question 1. Screenshot](screenshots/005-edit-page-1.png)
*Page with “Question 1” caption above a heading “Edit question”.

A secondary heading, “Question text”, comes directly before the hint text “Ask a question the way you would in person. For example ‘What is your address?’” and then a text input.

A second secondary heading, “Hint text (optional)”, followed by hint text “You can use hint text if you need to explain the format the answer should be in, or where to find the information you’ve asked for.” and then a text input.

Next is a secondary heading, “What kind of answer do you need to this question?”, which has the hint text “The answer will be checked to make sure it’s in the selected format.” Below are radio buttons that determine the input type required:

- Single line of text (selected)
- Multiple lines of text
- Number
- Address
- Date
- Email address
- National Insurance number
- Phone number
The page ends with a green “Save and add next question” button next to a grey “Save and preview question” button.
Below is a blue link “Go to form overview”.

On the right side of the screen there is a secondary heading “Question preview” above a link to “Preview question in a new tab”.

Below the link is a smaller version of an empty GOV.UK service page within an iframe. It shows the GOV.UK logo on a black header. Within the body of the page is a disabled green ‘Continue’ button.

<br>

### Edit question 2 - saved question
![edit question 2 - saved question. Screenshot](screenshots/006-edit-page-2-saved.png)
*Page with “Question 2” caption above a heading “What is your date of birth?”.*

The first text input contains the text that appears as the pages heading, “What is your date of birth?”.

The second text input with the secondary heading label “Hint text (optional)” has the text “Date of birth” in the text input.

The ‘Date’ radio is now selected.

The page ends with a green “Save and add next question” button next to a grey “Save and preview question” button. Below the green button is a red "Delete question" button
Below is a blue link “Go to form overview”.

On the right side of the screen the iframe has now updated to include the question text “What is your date of birth?” and displays the date component underneath with inputs for ‘Day’, ‘Month’ and ‘Year’. The green “Continue” button is still disabled.

<br>

### Delete a question
![delete a question. Screenshot](screenshots/005-delete-question-1.png)
*Page with “Are you sure you want to delete this question?” as the heading.*

There are two radio options, “Yes” and “No”. Below is a green “Continue” button.

<br>

### Add and edit your questions - with questions

![Add and edit your questions - with questions. Screenshot](screenshots/007-form-index-questions.png)
*Page with “Apply for a juggling licence” caption above the heading that says “Add and edit your questions”.*

There is a purple status tag with a descriptor 'draft' to let users know this is a draft form. 
There is a green “Add a question” button.
There is a secondary heading, “Your questions" and below is a link "Preview the form in a new tab". 

There is a list of questions created and saved for this form. 
The first question is "What is your name?". To the right is a grey “Move down” button and below it a link "edit".
There is a section break
The second question is "What is your date of birth?". To the right is a grey “Move up” button, next to it a grey "Move down" button. Bellow the "Mode down" is a link "edit".
There is a section break
The third queston is "What is your National Insurance number?". To the right is a grey "Move up" button and below is a link "edit".

<br>

### Add a declaration 
![add a declaration. Screenshot](screenshots/101-edit-page-check-answers.png)
*Page with “Apply for a juggling licence” caption above the heading that says “Add a a declaration".*

There is a paragraph describing the check your answers page is to help the form creator, “When someone has answered all the questions in your form, they will be shown a page that lists all of their answers. The page will ask them to check their answers before they submit the form."

The next paragraph describes what a declaration is "You can add a declaration to this page. A declaration is some content that people must confirm they understand and agree to before they submit the form. 

Another paragraph follows describing the declaration "You might want to add a declaration if you need people to confirm they have provided accurate information, or that they understand the consequences of providing false information. 

This is followed by a third level heading "Example", and below an inset text with the example "By submitting this form your are confirming that, to the best of your knowledge, the answers you are providing are correct."

There is a secondary heading label, “Enter a declaration for people to agree to (optional)" before a text area with a character counter, “You have 2,000 characters remaining”, giving form creators an idea of how much they have left of a 2,000 character limit.

At the end of the page is a green “Save and continue” button along side a grey “Save and preview” secondary action button.

On the right side of the screen there is a secondary heading, “Page preview”.

The iframe includes the title “Check your answers before submitting your form".  There is also a secondary heading, “What happens next”, above where the text input content provided on the left would appear.








