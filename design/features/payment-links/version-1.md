# Payment link v1

## Status

Date created: *2024-04-30*  

Developed  

___

## Contents

- [Status](#status)
- [Contents](#contents)
- [What](#what)
- [Key decisions](#key-decisions)
- [Designs](#designs)
- [Research focus](#research-focus)

___

## What

### As-is

- With the introduction of detailed guidance form creators can now add links to pages - this in theory allows them to add payment links they generate in GOV.UK Pay - but is not part of the form validation or checks
- Using the WHN information form creators can add links - this in theory allows them to add payment links they generate in GOV.UK Pay - but is not part of the form validation or checks  

### To-be

- Form creators can add payment links they have created via GOV.UK Pay
- GOV.UK Forms will handle the journey to make it consistent across forms - this means payments are taken after the form has been submitted (this aligns us with MoJ Forms, and means we don’t need to wait or worry about any work or timelines of the GOV.UK Pay team)  

___

## Key decisions

- We will only offer the opportunity to add a GOV.UK Pay payment link, meaning we will not support other payment providers
  - we will validate the URL provided to make sure it meets the expected GOV.UK Pay link structure  
- We will make the task of adding a payment link ‘optional’ for every form created adding it as a new task on the “Create a form” task list screen  
  - this new ‘optional’ task won’t have an impact on the task completed count used to inform form creators of how many tasks they have outstanding  
- We will give basic guidance as is helpful for our users, we don’t want to replicate anything explained by the GOV.UK Pay documentation or journey  
- GOV.UK Forms will generate a unique reference number for every form submission  
  - this will be included in the submission email sent to the processing email address  
  - this will be included on the confirmation screen  
  - this will be included in the body of the confirmation email, if a form filler chooses to receive it  
  - if a payment link is added, we will include this link in the confirmation email  
- We will align the journey and design with MoJ Forms as our first iteration  
  - using the blue banner with content “You still need to pay” to make it clear to form fillers that they have not finished yet  
  - we will include a clear call to action on this new confirmation screen to make a payment  

___

## Designs

### Create a form - new ‘optional tasks’ section

![Create a form task list page showing new ‘optional’ task to “Add a link to a payment page on GOV.UK Pay”. Screenshot](./screenshots-v1/001-create-a-form-optional-task.png)


### Add a link to a payment page on GOV.UK Pay

![Add a link to a payment page on GOV.UK Pay page showing guidance to help form creators set up a payment link. Screenshot](./screenshots-v1/002-add-a-link-to-a-payment-page-on-govuk-pay.png)


#### Add a link error summary

![“There is a problem” error summary notification. Screenshot](./screenshots-v1/002-add-a-link-to-a-payment-page-on-govuk-pay-error-summary.png)
*The error message that is linked to the input says “Enter a link in the correct format, like https​://www.gov.uk/payments/organisation/service”*  

### Create a form - payment link added

![Create a form task list page showing green “Your payment link has been saved” success notification at the top. Screenshot](./screenshots-v1/003-create-a-form-added-payment-link.png)


#### Payment link successfully added notification

![“Your payment link has been saved” success notification. Screenshot](./screenshots-v1/003-success-notification.png)


### Create a form - landing on the task list page that already has a payment link  

![Create a form task list page showing “Add a link to a payment page on GOV.UK Pay” marked as ‘completed’. Screenshot](./screenshots-v1/004-create-a-form-return.png)


___

## Preveiwing the form fillers journey

### Confirmation screen preview 

![You still need to pay heading inside a blue box replacing the usual green confirmaiton box. Screenshot](./screenshots-v1/1000-preview-confirmation-still-need-to-pay.png)


### Confirmation email   

![Email inbox showing an test email confirming submission that form fillers would receive. Screenshot](./screenshots-v1/1002-preview-test-email-with-payment-link.png)


### Example of a GOV.UK Pay payment link start page   

This is an example of a GOV.UK Pay start page. It shows what the form filler would see when they click through to make a payment. 
In this example it shows the service name, “Apply for a licence”, the task or name of the payment as set in GOV.UK Pay, “Pay for a parking permit”. There is no additional content added, but this can be done as part of setting up the payment link within GOV.UK Pay. There is a ‘continue’ button call to action to take the form filler into their payment journey.  

![Pay for a parking permit headed page with a green ‘continue’ button. Screenshot](./screenshots-v1/1001-preview-journey.png)


### Notes

- 

___

## Research focus

### To test:
- 

<br>

___

<br>

[Back to the top](#payment-link-v1)
