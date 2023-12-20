## Status 
Date created:   05.12.23

Developed
___

## Contents

- [Feature name]
  - [Status](#status)
  - [Contents](#contents)
  - [What we’re doing](#what-were-doing)
  - [Why we’re doing this](#why-were-doing-this)
  - [Key decisions](#key-decisions)
  - [Designs](#designs)
___

## What we’re doing
We’re making some changes to the GOV.UK Forms ‘Confirm that a form’s been submitted’ (or ‘Confirmation emails’) feature. This is in response to findings from usability testing with both form creators and form processors in sprint 41.

The research found that people were not noticing the new content we’d added to the existing ‘What happens next’ (WHN) and ‘Contact details’ pages in forms-admin. This new content explained that any content a form creator added to either of these pages would appear in a confirmation email **as well as** an on-screen confirmation page after someone submits a form.

We’re now iterating these 2 pages in forms-admin to make it clearer that any WHN or contact information a form creator adds will appear in 2 places  - the confirmation screen **and** a confirmation email (if requested, as this is an optional feature for form fillers).

As a result of the findings, we’re going to:

- change the page heading for the ‘Form submitted page’ and iterate the content (in forms-admin)
- iterate the content on the ‘Contact details for support’ page (in forms-admin) 
- make a minor tweak to the confirmation email itself (using the Notify email template) 

### Version 1 - confirmation emails feature (as-is)
See the [Mural designs for the first iteration of this feature](https://app.mural.co/t/gaap0347/m/gaap0347/1688563053078/f59d07f0cd2dca526768595d30228b4b0188ea32?wid=0-1700480040118)

#### ‘Form submitted page’ outlining what happens next - new paragraph added
On the existing ‘Form submitted page’ we added the following paragraph:
“This content will also be included in an email confirming that a form's been submitted - if people choose to receive this. The email will include the date and time of submission, and contact details for support. It will not contain a copy of someone's answers.”

This appeared below the main page content and example text, and above the text input field. 

#### ‘Contact details for support’ page - new paragraph added
On the existing ‘Contact details for support’ page we added the following paragraph: 
“It will also be included in an email confirming that a form's been submitted - if people choose to receive this. The email will include the date and time of submission. It will not contain a copy of someone's answers.” 

This appeared below the main content explaining that form creators must provide at least one way for people to get in touch, and above the ‘How can people get help with filling in this form?’ label and check boxes.

#### Confirmation email version 1 (Notify template)
The original version of this email contained the following content:

[H1] Your form has been successfully submitted

["Form name"] was successfully submitted at [time - 4:46pm] on [day - 3] [month - July] [year - 2023].
Thank you.

[Inset text] You cannot reply to this email. Use the contact details below if you need help with your form.

[H2] What happens next

[*Content will be whatever the form creator has specified on the 'Form submitted' page*]

[H2] Get help with your form

[*Content will be whatever the form creator has specified on the 'Provide contact details for support' page - email, phone or online contact link*]

### Version 2 - confirmation emails feature (to-be)

See [Mural designs for the second iteration of this feature](https://app.mural.co/t/gaap0347/m/gaap0347/1688563053078/f59d07f0cd2dca526768595d30228b4b0188ea32?wid=0-1700479967524) 

#### ‘Form submitted page’ outlining what happens next - changed page title and iterated content 
We’ve made the following changes: 

- Page title changed to “Add information about what happens next” - this is more accurate as any information form creators add here is no longer just included on the ‘form submitted page’
- Intro paragraph changed for accuracy - it referred to the page being “shown after someone has completed and submitted the form” but it will now be used in emails as well. Updated content says: “Add some information to tell people what will happen after they've submitted their form, and when - so they know what to expect.”
- Example has been moved up so it sits beneath the intro paragraph - it’s helpful for people to see some sample ‘what happens next’ copy up front to understand how this might be used
- Next paragraph uses bullet points to clarify that content will appear in 2 places, each of which is given equal weighting - this should help avoid the issue of people not noticing the confirmation email content
- Retained an extra paragraph about what else the confirmation email will include, in case this affects what a form creator decides to include here 

See Trello card: [Iterate content in forms-admin for confirmation email post testing](https://trello.com/c/BCge3DIm/1189-iterate-content-in-forms-admin-for-confirmation-email-feature-post-testing) 

#### ‘Contact details for support’ page - iterated content
We’ve made the following changes: 

- Added 2 bullet points to the second paragraph to make it clearer that whatever contact details form creators provide will now appear in 2 places - at the bottom of every page within the form, and on a confirmation email (if requested)
- Used the second bullet point to include the key information that a confirmation email will include - date and time a form was submitted
- Retained a shortened extra paragraph about what else the confirmation email will include, in case this affects what contact details a form creator decides to include here 

See Trello card: [Iterate content in forms-admin for confirmation email post testing](https://trello.com/c/BCge3DIm/1189-iterate-content-in-forms-admin-for-confirmation-email-feature-post-testing)

#### Confirmation email version 2 (Notify template)
See [Mural designs for this feature](https://app.mural.co/t/gaap0347/m/gaap0347/1688563053078/f59d07f0cd2dca526768595d30228b4b0188ea32?wid=0-1697551427587) 

We’ve made the following changes: 

- Updated second H2 to ‘Contact details’ instead of ‘Get help with your form’ - it's not really about getting help with the form itself at this stage. Form processors said that most form fillers will follow up about timescales etc. This heading is also consistent with the language used on the task list page and page title - 'Provide contact details for support'
- Retained the ‘thank you’ in the end, after some debate about whether this is necessary (or whether it might make someone think they don’t need to read any further) as it's not really house style to say please and thank you. Some users have previously said they appreciate a ‘thank you’ and expect to see this so we’re leaving it for now, particularly as it's in an email rather than the main product content.

See Trello card: [Change sub-heading content in confirmation email Notify template](https://trello.com/c/3ZMmBpDA/1190-change-sub-heading-content-in-confirmation-email-notify-template-following-testing?search_id=a6e7bfc5-2dcc-4fbe-a3a9-6b39598531bc)

___

## Why we’re doing this
We decided to address a couple of content-related issues that were highlighted during a first round of usability testing with form creators and form processors.

The main issue was that although most users previewed the form before editing it further - and therefore saw (or even responded to) the optional email confirmation question - they did not notice the extra content we’d added to the existing ‘What happens next’ (WHN) and ‘Contact details’ pages in forms-admin. 

Once this content was pointed out to people they found it easy to understand. However, we wanted to iterate the content to make it clearer to form creators that any content they add to the WHN or contact information pages will also appear in a confirmation email (if requested) as well as on the confirmation screen. 

___

## Key decisions
We decided to:

- change the page title for the WHN information - from ‘Form submitted page’ to ‘Add information about what happens next’ 
- iterate the WHN page content to make it clearer to form creators that any information they add here will be shown on a confirmation page as well as in a confirmation email (if requested) 
- iterate the ‘Provide contact details for support’ page content to make it clearer to form creators that any information they add here will be shown on a confirmation page as well as in a confirmation email (if requested) 
- make a small change to the email template in Notify - changing a subheading to ‘Contact details’ instead of ‘Get help with your form’

___

## Designs

### ‘Add information about what happens next’ page - new page title and updated content
The page title has been changed from ‘Form submitted page’ to ‘Add information about what happens next’. 

The content has been iterated to make it clearer that this content will now be shown in 2 places - an optional confirmation email as well as a confirmation screen. It uses a bulleted list to do this. 

![New page title and updated content for 'what happens next' page. Screenshot](/design/features/confirmation-email-for-form-fillers/screenshots-v2/what-happens-next-page-new-page-title-and-updated-content.png)

### ‘Provide contact details for support’ page - updated content
The content has been iterated to make it clearer that this content will now be shown in 2 places - an optional confirmation email as well as a confirmation screen. It uses a bulleted list to do this. 

![Updated content for 'contact details' page. Screenshot](/design/features/confirmation-email-for-form-fillers/screenshots-v2/provide-contact-details-for-support-page-updated-content.png)

### Confirmation email - Notify template
The second subheading in the updated confirmation email now says ‘Contact details’ instead of ‘Get help with your form’. (Screenshot shows design mock-up in Mural.) 

![New subheading shown on Mural mock-up of Notify template for confirmation email. Screenshot](/design/features/confirmation-email-for-form-fillers/screenshots-v2/confirmation-email-mural-mockup-notify-template.png)

___



