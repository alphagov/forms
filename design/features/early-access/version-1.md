#   Early Access Journey Designs

## Status

- Date created: *2023-11-9*
- Developed 

## Contents
- [Status](#status)
- [Key Decisions](#key-decisions)
- [Designs](#Designs)

## As is 
- There is currently no process in place for trial users to request an editor account. 

## To-be
- Early access journey enables trial users to request an editor account within the GOV.UK Forms. 

## Key Decisions
It was agreed that we'll build a minimum version that is needed for this journey, while making it available as soon as possible so that more trial users can be upgraded to an editor. 

Once we move from private beta, we'll design another version of early access where we wil be focusing on creating a self service model. In this process we will focus on automating some of the tasks adoption team currently takes place and create a model where we don't rely too much on the adoption team.

We are also using Auth0 for this journey. 

## Designs
- [Figma files for designs can be found here](https://www.figma.com/file/pCN39S9tIDlgicZ05Nj47J/Early-Access?type=design&node-id=337%3A3586&mode=design&t=0R6O7wWl9Alok9vs-1 "Figma files for designs can be found here")
- [Protoype can be found here](https://forms-prototypes-pr-201.herokuapp.com/product-pages)
<br>

### Get started page
![Get Started](/design/features/early-access/screenshots-v1/002.Get-started.png)

<br>

*This shows the “Get started” page and the following explanatory text: "GOV.UK Forms is a new platform that makes it easy to create accessible online forms for the GOV.UK website."*  

With this page, trial user can read and understand what they can do with a trial account and read more about what they need to do in order to become an editor. 

Once "Create a trial account button" is clicked the trial user is taken to "Auth0 login page"

### Trial account notification banner
![Trial account notification banner](/design/features/early-access/screenshots-v1/007.Trial-notification-banner.png)

<br>

Once the users are aunthenticated using the Auth0 login journey they are taken to the GOV.UK Forms landing page. 

Here we have a notification banner to inform the users that they need have a trial account. *It uses the following text "You have a trial account, you can create a form, preview and test it. You need an editor account to be able to make a form live and if the trial user want to become an editor they need to click "find out if you can upgrade to an editor account"*

Once the users click the link they are taken to "Requirements to upgrade to an editor account" page. 

### Requirements to upgrade to an editor account
![Requirements to upgrade to an editor account](/design/features/early-access/screenshots-v1/004.Requirements-page.png)

<br>

Requirements to upgrade to an editor account is created to help users understand what do they need to become an editor. 

On this page we have created a description and a list of requirements needed to become an editor and a check box asking the users if they meet these requirements. 

Once the check boxed is ticked, the users is then asked to click "Continue". Once "Continue" button is clicked user is taken to "What happens next" page. 

### What happens next page
![What happens next](/design/features/early-access/screenshots-v1/005.What-happens-next.png)

<br>
What happens next page infomrs users about the next steps in the early access journey. 

Here we are using a panel component with a text that says *We've sent you an email to request more information* 

Outside the panel component we incldued a "What happens next" title and a text that says *Check your email and reply with the information requested. we'll then get in contact with you to discuss the next steps. It may take up to 2 weeks.*

We also created a "Back to your forms" link to allow users go back.

At this stage users are directed to email where they hear from the adoption team. 

### Memorandum of Understanding page
![MOU](/design/features/early-access/screenshots-v1/003.Mou.png)

<br>

If the adoption team identifies that this user needs to sign MOU, they send a link to it via email. At this stage users are asked to click to that link and are taken to "Memorandum of Understanding page". In this page we have all the MOU document where user needs to read and sign. 

At the end of the back we have added a check box where it says *I agree to the MOU on behalf of my organisation*. Once checked the users are asked to click "Save and continue". Users are then taken to "Agreeing to MOU' page. 

### Agreeing to MOU
![Agreeing to MOU](/design/features/early-access/screenshots-v1/006.Agreeing-to-mou.png)

<br>

On this page we inform users that they have signed the MOU with a panel that says *You’ve agreed to the MOU*. We also added a "What happens next" title with a text saying *We’ll email you with any updates to the MOU that are made in the future.* 

At the top left hand corner we have also included a back button, allowing users to go back to their form. 

### "You have an editor account" Notification banner
![Notificaiton banner](/design/features/early-access/screenshots-v1/001.Editor-notification-banner.png)

<br>

Once the adoption team upgrades the user and the trial user sign back in to their GOV.UK Forms account, they see a notification banner that says *You now have an editor account. You can create a form and make it live.*  

They also see a button that says "Create a form". Once clciked user is taken to GOV.UK forms landing page. 


## Some of the changes we have done after the research;

<br>

- We have created some content changes for the "Get started" , "Requirements to become an editor" , "What happens next page"

[Back to the top](#early-access-journey-designs)
