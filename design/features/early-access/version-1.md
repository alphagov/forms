#   Early Access Designs
## Status

- Date created: *2023-11-9*
- Developed 

## Contents
- [Status](#status)
- [Decisions](#decisions)
- [Designs](#Designs)

## What 

## As is 
- There is currently no process in place for trial users to request an editor account. 

## To-be
- Early access journey enables trial users to request an editor account within the GOV.UK Forms. 

## Key Decisions
It was agreed that we'll build a minimum version that covers the basic functionality needed for this journey, while making it available as soon as possible so that more trial users can be upgraded to an editor. 

Once we move from private beta, we'll design another version of early access where we wil be focusing on creating a self service model. In this process we will focus on automating some of the taks adoption team currently takes place and crate a model where users can upgrade to an editor account without an action from the adoption team. 

We are also using Auth0 for this journey. 

## Designs
[Figma files for designs can be found here](https://www.figma.com/file/pCN39S9tIDlgicZ05Nj47J/Early-Access?type=design&node-id=337%3A3586&mode=design&t=0R6O7wWl9Alok9vs-1 "Figma files for designs can be found here")
<br>
<br>

### Get started page
Created a get started page to help users understan what we offer at GOV.UK Forms.
![Get Started](/design/features/early-access/screenshots-v1/002.Get-started.png)

*This shows the “Get started” page and the following explanatory text: "GOV.UK Forms is a new platform that makes it easy to create accessible online forms for the GOV.UK website." *  

With this page, trial user can read and understand what they can do with a trial account and read more about what they need to do in order to become an editor. 

Once "Create a trial account button" is clicked the trial user is taken to "Auth0 login page"

### Trial account notification banner
Added a notification banner informing users that they have a trial account.
![Trial account notification banner](/design/features/early-access/screenshots-v1/007.Trial-notification-banner.png)

Once the users are aunthenticated using the AUTH0 login journey they are taken to the GOV.UK Forms landing page. 

*Here we have a notification banner to inform the users that they need have a trial account. It uses the following text "You have a trial account, you can create a form, preview and test it. You need an editor account to be able to make a form live and if the trial user want to become an editor they need to click "find out if you can upgrade to an editor account"*

Once the users click the link they are taken to "Requirements to upgrade to an editor account" page. 

### Requirements to upgrade to an editor account
Created a page listing out all the requirements GOV.UK Forms team have to updgrade trial accounts into an editor account.
![Requirements to upgrade to an editor account](/design/features/early-access/screenshots-v1/004.Requirements-page.png)

### What happens next page
Created a page informing users about the next step
![What happens next](/design/features/early-access/screenshots-v1/005.What-happens-next.png)

### Memorandum of Understanding page
MOU page, where we ask a specific group of users to sign this.
![MOU](/design/features/early-access/screenshots-v1/003.Mou.png)

### Agreeing to MOU
Created a page informing users, they have signed the MOU.
![Agreeing to MOU](/design/features/early-access/screenshots-v1/006.Agreeing-to-mou.png)

### "You have an editor account" Notification banner
Once the users have gone through the early access journey and sign back in to their GOV.UK Forms account, we added a notification banner saying that they have an editor account. 
![Notificaiton banner](/design/features/early-access/screenshots-v1/001.Editor-notification-banner.png)

