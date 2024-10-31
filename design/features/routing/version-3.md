# Branching and exit pages iteration 1

## Status

Date created: *2023-10-24*  

Developed  

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

- We're only going to allow routing to be set up from a radio button answer type 
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
  - **We are yet to agree if the secondary route should be deleted**
- If the route’s start question answer type is changed from a radio option, the route will be deleted. This includes:  
  - the answer type being changed  
  - the option for “People can only select one option” being unselected on the “Create a list of options” screen, making the question a checkbox rather than a radio-type question  

## Designs

### New “Add a question route” journey and view on questions list page

!["Add and edit your questions" page with new grey “Add a question route” button next to the green “Add a question” button. Screenshot.](https://github.com/alphagov/forms/assets/35372982/700ad8f7-0fa7-4484-b636-2263beb141d2)
*As part of the list of questions added to the form there's a new row, with the row heading “Question 2’s route”. To the right of this are the start question, the answer to base the route on and the page to take the user to if the answer is chosen. There's an edit link at the end of the row.*

### Notes

- 

___

## Research focus

- To understand the high-level user needs when using branching (we will learn more detailed needs when we see them using our designs in action)
- To understand the user’s mental model for branching (where and how to implement it)
- To learn what language people use around branching
- For those who have their own dept platform - find out how they’ve implemented and what they’ve learned

[Research planning and discussion guide](https://drive.google.com/drive/folders/1Jb7oUSfBXBamRgFkIjxf_DMRZEK5sfnM)

___

[Back to the top](#branching-and-exit-pages-iteration-1)
