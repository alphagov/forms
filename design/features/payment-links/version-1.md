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

<br>

## What

### As-is

- With the introduction of detailed guidance form creators can now add links to pages - this in theory allows them to add payment links they generate in GOV.UK Pay - but is not part of the form validation or checks
- Using the WHN information form creators can add links - this in theory allows them to add payment links they generate in GOV.UK Pay - but is not part of the form validation or checks  

### To-be

- Form creators can add payment links they have created via GOV.UK Pay
- GOV.UK Forms will handle the journey to make it consistent across forms - this means payments are taken after the form has been submitted (this aligns us with MoJ Forms, and means we don’t need to wait or worry about any work or timelines of the GOV.UK Pay team)  


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

<br>

## Designs

### screens


### Notes

- 

___

<br>

## Research focus

### To test:
- 

<br>

___

<br>

[Back to the top](#payment-link-v1)
