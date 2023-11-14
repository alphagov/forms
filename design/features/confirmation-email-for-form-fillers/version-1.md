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

- form fillers do not get any more confirmation of a submission than the confirmation screen  
- currently form fillers are unable to get a copy of their submission sent to them  
- if a form filler wants to save their submission data they can “print” screen on the check your answers  

### To-be

- form fillers receive a confirmation of their submission being successfully sent (MVP)  
- form fillers can get a copy of their submission data sent to them (not MVP)  
- form creators can control different aspects of confirmation emails such as, including WHN information (not MVP)  


## Key decisions

It was agreed that we'll build a minimum version. This will involve a way for form fillers to decide if they receive an email confirming their submission or not, meaning we will only inform form creators of where the information they add to their form will be provided.  

As part of our first iteration:  

- We’ll include journey for form fillers to opt-in/out of receiving a confirmaiton email
- We’ll create guidance for form creators about what the confirmation email does and does not do - with examples
- The email contents will be limited to:
  - date and time of submission
  - form name
  - thank you
  - “do not reply” messaging
  - what happens next information
  - support contact details

<br>

## Design for form fillers

What are we doing... 

### Check your answers page

![Check your answers before submitting summary screen with new email confirmation question. Screenshot](https://github.com/alphagov/forms/assets/35372982/7ac041dd-0112-4e73-866c-a9f44243f731)
*Do you want to get an email confirming your form has been submitted?*

![Check your answers before submitting summary screen with new email confirmation question expanded with input for email address. Screenshot](https://github.com/alphagov/forms/assets/35372982/06fa052d-2cfd-4d31-aaea-1081ce02e187)
*Do you want to get an email confirming your form has been submitted?*

### Email examples

![Access to work plus referral confirmation email example. Screenshot](https://github.com/alphagov/forms/assets/35372982/cf4d3bfd-b0d5-41b8-a8fc-281431861eee)
*caption*

![Apply for a county parish holding confirmation email example. Screenshot](https://github.com/alphagov/forms/assets/35372982/a884ec01-d0c8-4509-a6d1-09881530adf0)
*caption*

<br>

## Design for form creators

What are we doing... 

### Form submitted page

![Form submitted page. Screenshot](https://github.com/alphagov/forms/assets/35372982/24eabfbc-f961-43ea-8b4a-cc764af65a11)
*caption*

### Provide contact details for support

![Provide contact details for support. Screenshot](https://github.com/alphagov/forms/assets/35372982/06fa052d-2cfd-4d31-aaea-1081ce02e187)
*caption*

<br>

## Notes

We know that we will have to return to this feature later to include:  

- controls for form creators  
  - allow them to dictate if the WHN information is or is not included in the confirmation email  
  - give them a way to make confirmation emails mandatory for all users  
  - explore if we should allow them to decide their own subject line for the emails  
  - explore if we should let them control if submission data is or is not included in a confirmation email
    - does the submission copy need to act as a legal proof (due to policy. This will dictate file types such as PDF over .txt)
  - explore options to create most customised emails
  - explore generated submission references  
  - understand if we can or should offer alternative confirmation messaging such as SMS  
  - understand if there is any need for metrics on confirmation emails
    - number of times form fillers request an email confirming their submission (useful for our team, but is it useful for form creators?)
    - number of failed deliveries (useful for our team, but is it useful for form creators?)
  
- better experience for form fillers  
  - if we collect an email within the journey we should offer that as the email for their confirmation to be sent to  
  - a way to receive a copy of their answers (on submission)  
  - a way to download a copy of their answers (pre/post submission)  
  - validate an email address (without making a user type it multiple times)  
  - explore if we should validate that they have access to the chosen email address (such as one time code)  

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
      - How long would they keep it etc  
- Is there anything else they would expect or feel needs to be included for the email to be useful?  
- Do they understand the information provided and what it means to their situation?  
- Do people need copies of their answers for reference?  

[Form compeleters questions / assumptions to test (Google working doc)](https://docs.google.com/document/d/1iVKcNV1S2jLwT6qGUFx83TKavX8sk3lqeje8FCJSv3Y/edit?usp=sharing)  

[Discussion Guide: Confirmation Emails - Form Builders (Google doc)](https://docs.google.com/document/d/1A25i13xc5yiPdWbYDJHNi64_XIwxpPL_KWc_7I3zMcs/edit?usp=sharing)  
[Discussion Guide: Confirmation Emails - Processors (Google doc)](https://docs.google.com/document/d/1JI6xwDqkAdaEFaJmE0za9UBRY8xyY-Sbmlh2xv9HEaQ/edit?usp=sharing)  

### Update: what we found through testing  

[Playback - User Research - Confirmation Emails (Google slides)](https://docs.google.com/presentation/d/1652cpRz963L3nWHxn1dhlV2WrPJM4g4VnBx4RQhjv_s/edit?usp=sharing)  
[Playback: User Research on Confirmation Emails (Video)](https://drive.google.com/drive/folders/1DiWgtUJ_4pnJDXCYXeZgSqWvMHJHOvbd)  

<br>

___

<br>

[Back to the top](#confirmation-email-for-form-fillers-v1)
