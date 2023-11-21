# Confirmation email for form fillers v1

## Status

Date created: *2023-11-07*  

Developed  

___

## Contents

- [Status](#status)
- [Contents](#contents)
- [What](#what)
- [Key decisions](#key-decisions)
- [Design for form fillers](#design-for-form-fillers)
  - [Check your answers page](#check-your-answers-page)
  - [Email examples](#email-examples)
- [Design for form creators](#design-for-form-creators)
  - [Form submitted page](#form-submitted-page)
  - [Provide contact details for support](#provide-contact-details-for-support)
- [Notes](#notes)
- [Research focus](#research-focus)

___

<br>

## What

### As-is

- The only confirmation of a submission that form fillers get is the confirmation screen that appears after they click ‘Agree and submit’
- Currently form fillers are unable to get a copy of their submission sent to them  
- If a form filler wants to save their submission data they can ‘print’ screen on the check your answers page  

### To-be

- Form fillers receive a confirmation of their submission being successfully sent [MVP]  
- Form fillers can get a copy of their submission data sent to them [not MVP]  
- Form creators can control different aspects of confirmation emails, such as including ‘what happens next’ (WHN) information [not MVP]  


## Key decisions

It was agreed that we’ll build a minimum version. This will involve a way for form fillers to choose whether to receive an email confirming their submission or not. 

We’ll explain to form creators that certain information they add to their form will be provided in this email.  

As part of our first iteration:  

- We’ll include journey for form fillers to opt in/out of receiving a confirmation email
- We’ll create guidance for form creators about what the confirmation email does and does not do - with examples
- The email contents will be limited to:
  - date and time of submission
  - form name
  - thank you
  - ‘do not reply’ messaging
  - ‘what happens next’ information
  - support contact details

<br>

## Design for form fillers

To get us ready for early access we wanted to make the smallest iteration with the most impact. We therefore agreed to only add a way for form fillers to opt in or out of receiving an email confirming a successful submission. This option will be included on the “Check your answers before submitting your form” page.

### ‘Check your answers’ page

![Check your answers before submitting summary screen with new email confirmation question. Screenshot](https://github.com/alphagov/forms/assets/35372982/7ac041dd-0112-4e73-866c-a9f44243f731)  
*This screen shows the new “Do you want to get an email confirming your form has been submitted?” question with ‘Yes’ and ‘No’ radio options.*

We want it to be clear why form fillers are being asked this question, so we've included hint text:  
> We'll only use your email address to send a confirmation that your form's been successfully submitted. It will not contain a copy of your answers.  

This question is mandatory and if no option is selected we’ll reload the screen with an error summary and message.  

![Error summary when a user doesn’t select a radio option for email confirmation. Screenshot](https://github.com/alphagov/forms/assets/35372982/c0504aa6-7983-4dd0-8293-29d97fc18e5b)  
*The error summary shows “There is a problem”. The detailed error message shows “Select ‘Yes’ if you want to get an email confirming your form has been submitted” to help form fillers understand what’s gone wrong.*

![Check your answers before submitting summary screen with new email confirmation question expanded with input for email address. Screenshot](https://github.com/alphagov/forms/assets/35372982/06fa052d-2cfd-4d31-aaea-1081ce02e187)  
*This screen now shows the “Do you want to get an email confirming your form has been submitted?” question with the ‘Yes’ radio expanded to reveal a new input.*

Because the form filler has selected ‘Yes’ - meaning they want to get an email confirming their form has been submitted - they're now asked: 
> What email address do you want us to send your confirmation to?  

This question is also mandatory, where the form filler has selected the ‘Yes’ radio. If they have not provided a valid email the screen will reload with a new error summary and message. 

![Error summary when a user doesn’t input a valid email address for email confirmation to be sent to. Screenshot](https://github.com/alphagov/forms/assets/35372982/82f8be47-8827-4dfe-8d0d-e188510d54fb)  
*The error summary shows “There is a problem”. The detailed error message shows “Enter an email address in the correct format, like name@example.com” to help form fillers understand what’s gone wrong.*

<br> 

### Email content structure  

Emails will come from the “GOV.UK Forms” email address.  

Email subject lines will be the same for all emails at this point: “Your form has been successfully submitted”.  

> ## Your form has been successfully submitted  
> "[form_name]" was successfully submitted at 4:46pm on 3 July 2023.  
> 
> Thank you.  
>
> You cannot reply to this email. Use the contact details below if you need help with your form.  
>
> ### What happens next  
> [Content will be whatever the form creator has specified on the 'Form submitted' page]  
>
> ### Contact details  
> [Content will be whatever the form creator has specified on the 'Provide contact details for support' page - email, phone or online contact link]  


#### Email examples

The emails will include:

- name of the form that the form filler has completed  
- date and time the form filler submitted their form  
- “Thank you” - this can add value to people completing forms, showing appreciation for their time, even if it’s a mandatory form    
- information telling the form filler that they cannot reply to this email and referring them to the contact details provided later in the email
- information about ‘What happens next’ which the form creator has added to their form's confirmation page  
- contact information that the form creator has added to support their users  
  
![Access to work plus referral confirmation email example. Screenshot](https://github.com/alphagov/forms/assets/35372982/cf4d3bfd-b0d5-41b8-a8fc-281431861eee)  
*This email shows an outline of the content and format that a typical email confirming that a submission's been sent might look like. This example shows information DWP might use for one of their forms.*

![Apply for a county parish holding confirmation email example. Screenshot](https://github.com/alphagov/forms/assets/35372982/a884ec01-d0c8-4509-a6d1-09881530adf0)  
*This email shows an outline of the content and format that a typical email confirming that a submission's been sent might look like. This example shows information Defra might use for one of their forms.*

<br>

## Design for form creators

Giving form fillers control over whether or not they receive an email confirmation meant we needed to tell form creators about any information they provide which will be included in this email - and to make sure we do this at the appropriate stage of their form-creation journey. We decided that this would be at the point form creators add or edit their content for the "Information about what happens next" and "Contact details for support" pages. 

### Form submitted page

![Form submitted page. Screenshot](https://github.com/alphagov/forms/assets/35372982/24eabfbc-f961-43ea-8b4a-cc764af65a11)  

We’ve added new content to this screen, just above the textarea input:

> This content will also be included in an email confirming that a form's been submitted - if people choose to receive this. The email will include the date and time of submission, and contact details for support. It will not contain a copy of someone's answers.

### Provide contact details for support

![Provide contact details for support. Screenshot](https://github.com/alphagov/forms/assets/35372982/0d928780-b80d-4f63-a09b-81fc69409259)

We’ve added new content to this screen, just above the “How can people get help with filling in this form?” question:

> It will also be included in an email confirming that a form's been submitted - if people choose to receive this. The email will include the date and time of submission. It will not contain a copy of someone's answers.


<br>

## Notes

We know that we’ll have to return to this feature later to include the following:  

- Controls for form creators:  
  - Allow them to dictate if the WHN information is or is not included in the confirmation email  
  - Give them a way to make confirmation emails mandatory for all users  
  - Explore if we should allow them to decide their own subject line for the emails  
  - Explore if we should let them control whether submission data is or is not included in a confirmation email
    - Does the submission copy need to act as a legal proof (due to policy. This will dictate file types such as PDF over .txt)
  - Explore options to create more customised emails
  - Explore generated submission references  
  - Understand if we can or should offer alternative confirmation messaging such as SMS  
  - Understand if there is any need for metrics on confirmation emails
    - Number of times form fillers request an email confirming their submission (useful for our team, but is it useful for form creators?)
    - Number of failed deliveries (useful for our team, but is it useful for form creators?)
  
- A better experience for form fillers:  
  - If we collect an email within the journey we should offer that as the email for their confirmation to be sent to  
  - A way to receive a copy of their answers (on submission)  
  - A way to download a copy of their answers (pre/post submission)  
  - Validate an email address (without making a user type it multiple times)  
  - Explore if we should validate that they have access to the chosen email address (such as one-time code)  

___

<br>

## Research focus

### Things we plan to focus on in testing:  
- Do you want to get an email confirming your form has been submitted? Journey  
  - Are users likely to request a confirmation email?  
  - Does the content explain enough of what they should expect?  
  - Are they likely to use the same email as earlier in the journey… and do users pick up that they’ve already been asked for their email?  
- Confirmation emails - format and information contained in these messages.  
  - Do users feel like the confirmation email adds any value to them?  
    - If so, what and why?  
    - What will they do with the email after receiving it?  
      - How long would they keep it? etc  
- Is there anything else they would expect or feel needs to be included for the email to be useful?  
- Do they understand the information provided and what it means to their situation?  
- Do people need copies of their answers for reference?  

[Form completers questions / assumptions to test (Google working doc)](https://docs.google.com/document/d/1iVKcNV1S2jLwT6qGUFx83TKavX8sk3lqeje8FCJSv3Y/edit?usp=sharing)  

[Discussion Guide: Confirmation Emails - Form Builders (Google doc)](https://docs.google.com/document/d/1A25i13xc5yiPdWbYDJHNi64_XIwxpPL_KWc_7I3zMcs/edit?usp=sharing)  
[Discussion Guide: Confirmation Emails - Processors (Google doc)](https://docs.google.com/document/d/1JI6xwDqkAdaEFaJmE0za9UBRY8xyY-Sbmlh2xv9HEaQ/edit?usp=sharing)  

### Update: what we found through testing  

[Playback - User Research - Confirmation Emails (Google slides)](https://docs.google.com/presentation/d/1652cpRz963L3nWHxn1dhlV2WrPJM4g4VnBx4RQhjv_s/edit?usp=sharing)  
[Playback: User Research on Confirmation Emails (Video)](https://drive.google.com/drive/folders/1DiWgtUJ_4pnJDXCYXeZgSqWvMHJHOvbd)  

<br>

___

<br>

[Back to the top](#confirmation-email-for-form-fillers-v1)
