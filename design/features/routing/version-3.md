# Branching and exit pages iteration 1

## Status

Date created: *2024-10-24*  

Developing  

___

## Contents

- [Status](#status)
- [Contents](#contents)
- [What](#what)
- [Key decisions](#key-decisions)
- [Designs](#designs)
  - [Breaking change errors](#breaking-change-errors)
  - [Edit answer type warning](#edit-answer-type-warning)
  - [Notes](#notes)
- [Research focus](#research-focus)

___

<br>

## What

### As-is

- 1 question can have 1 answer (radio only) that can skip one or more questions

### To-be

- A question can have one radio answer that skips one or more questions - with the option to apply skip logic to any question after the trigger question.  
- A question can have one radio answer that takes the form filler out of the form journey, showing them an ‘exit page’ with custom content created by the form creator. 


## Key decisions

- We’re only going to allow routing to be set up from a radio button answer type 
- Only one route, branch or ‘exit page’ can be set up for each question
  - A question can be routed to and then routed from
  - A question cannot have multiple routes from it
- We have considered multiple routes from a single question, but have deprioritised for our first development 
- We’ll continue to prioritise errors for breaking changes, and will try to inform form creators of orphaned questions but not force them to fix these 
- We’ll continue to show breaking errors previosuly found and agreed 
- We’ll continue to stop a form being made ‘Live’ without the breaking change errors being resolved 
- We’ll not allow a creator to change the question the route is based on when editing a route 
  - The user should delete a route in this situation, as they’ll need to select all the different parts of the route
  - This will also be true at the time of review (checking a questions routes on the summary card list view) 
- Moving a page that has a route attached (meaning the start question) will also move the initial skip route, but will not impact the secondary route as this should be associated with a different question
  - Moving a page with a secondary route attached will also move the associated route
- If the route start question is deleted, the route will also be deleted
  - the secondary route should also be deleted
  - any exit pages attached to the route should be deleted, until we have the option to share exit pages across multiple routing questions
- If the route’s start question answer type is changed from a radio option, the route will be deleted. This includes:  
  - the answer type being changed  
  - the option for “People can only select one option” being unselected on the “Create a list of options” screen, making the question a checkbox rather than a radio-type question
- When a form creator has a route that ends on the “Check your answers before submitting” page, if they add any new questions to their form the original route will still take the person to the “Check your answers before submitting” page
  - It is up to the form creator to make changes to their route if they now need the form filler to answer the new questions
- As with the current skip routing, if a form creator moves pages up or down they can move them in or out of a branch route
- **TBC: Can a question have an override from a route, while also being a route start?**

## Designs

### Add and edit your questions

!["Add and edit your questions" page with grey “Add a question route” button next to the green “Add a question” button. Screenshot.](screenshots-v3/001-create-a-form.png)
*Draft form with a summary list showing questions added to the form “Apply for a juggling licence”.*  

The questions are each a new numbered row in the summar list. 

> 1 What’s your name?
> 2 Where were you born?
> 3 What’s your date of birth?
> 4 What’s your address?

Each row has a button to either move the question ‘up’ or ‘down’ in the forms order. Question 1 “What’s your name?” only has a “Move down” button, while question 4 “What’s your address?” only has a “Move up” button.  
Each row also has a blue ‘edit’ link that takes the form creator to edit the relevant question.  

#### Add and edit your questions with question routes 

!["Add and edit your questions" page. Screenshot.](screenshots-v3/001-create-a-form-question-route-created.png)
*Draft form with a summary list showing questions and question routes added to the form “Apply for a juggling licence”.*  


### Add a route from a question   

!["Add a route from a question" page. Screenshot.](screenshots-v3/002-add-route-from-question.png)
*Something about the new content and other stuff on the screen*  


### Edit route 1  

!["Edit route 1" page. Screenshot.](screenshots-v3/003-edit-route-1.png)
*Something about summary list of the quesiton and the inputs*  

#### Edit route 1 with “is answered as” dropdown open

!["Edit route 1" page with “is answered as” dropdown open. Screenshot.](screenshots-v3/003-edit-route-1-is-answered-as.png)
*Something about the dropdown choices*  

#### Edit route 1 with “take the person to” dropdown open

!["Edit route 1" page with “take the person to” dropdown open. Screenshot.](screenshots-v3/003-edit-route-1-take-the-person-to.png)
*Something about the dropdown choices*  


### Edit question 2’s route 

!["Edit question 2’s route" page playing back the recently created route 1. Screenshot.](screenshots-v3/005-edit-question2s-route.png)
*Something about the summary list*  

#### Edit question 2’s route with branching

!["Edit question 2’s route" page now showing the branching. Screenshot.](screenshots-v3/005-edit-question-2s-route-branch.png)
*Something about the summary list*  


### Set questions to skip

!["Set questions to skip" page. Screenshot.](screenshots-v3/006-set-questions-to-skip.png)
*Something about the new screen and content*  

#### Set questions to skip with “After the person answers” dropdown open

!["Set questions to skip" page with “After the person answers” dropdown open. Screenshot.](screenshots-v3/006-set-questions-to-skip-after-question.png)
*Something about the dropdown*  

#### Set questions to skip with “take them to” dropdown open

!["Set questions to skip" page with “take them to” dropdown open. Screenshot.](screenshots-v3/006-set-questions-to-skip-take-the-person-to.png)
*Something about the dropdown*  


### Edit exit page

!["Edit exit page" page. Screenshot.](screenshots-v3/006-set-questions-to-skip.png)
*Something about the new screen and content*  

___

## Research focus

- To understand the high-level user needs when using branching (we will learn more detailed needs when we see them using our designs in action)
- To understand the user’s mental model for branching (where and how to implement it)
- To learn what language people use around branching
- For those who have their own dept platform - find out how they’ve implemented and what they’ve learned

[Research planning and discussion guide](https://drive.google.com/drive/folders/1Jb7oUSfBXBamRgFkIjxf_DMRZEK5sfnM)

### What we tested

[User research session Oct 24 (Mural board)](https://app.mural.co/t/gaap0347/m/gaap0347/1729773162641/fbe698a2b44f833842196c252bb254abbb806042)

___

[Back to the top](#branching-and-exit-pages-iteration-1)
