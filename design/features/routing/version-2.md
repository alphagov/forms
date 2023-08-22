# Simple routing v2

## Status

Date created: *2023-08-16*  

Developed  

___

## Contents

- [Status](#status)
- [Contents](#contents)
- [What we’re doing](#what-were-doing)
- [Why we’re doing this](#why-were-doing-this)
- [Key decisions](#key-decisions)
- [Designs](#designs)

___

<br>

## What we’re doing

We’re making some changes to the GOV.UK Forms simple routing feature in response to findings from our first round of usability testing (sprint 30).

As a result of the findings, we’re going to:

1. change the criteria for showing the ‘Add a question route’ button so that it’s visible at all times
2. create a new version of the routing start page for users who click on this button before they meet any or all of the criteria for creating a route 
3. clarify what is / is not possible with simple routing
4. clarify the difference between optional questions and routing

<br>

### Version 1 simple routing feature (as-is) 

#### Criteria for showing the ‘Add a question route’ button 

The ‘Add a question route’ button appears at the top of the ‘Add and edit your questions’ page only when certain criteria are met. 

The criteria are that the form must have: 

- 2 or more questions
- at least one question where people must select a single item from a list of options

<br>

#### How we explain what is / is not possible with simple routing 

We specify on the ‘Add a question route’ page that you can only create a route from ‘select from a list of options’ questions. 

The wording is: “A route can only start from a question where people select one item from a list”. 

<br>

#### How we present the difference between optional questions and routing 

On the ‘Edit question’ page we have a check box that form creators can select if they want to make a question optional. 

The wording is: “Make this question optional so people can skip it”. 

The explanatory text is “‘(optional)’ will be added to the end of the question text”. 

<br>

### Version 2 simple routing feature (to-be) 

#### Criteria for showing the ‘Add a question route’ button

- The ‘Add a question route’ button will now be visible at all times, even if a form does not meet the criteria
- We’ll create different content for the routing start page depending on whether: 
    - routing criteria are not met and no other routes exist
    - routing criteria are not met but at least one other route exists
    - there’s one potential start question for a route
    - there are 2 to 10 potential start questions for a route
    - there are 11+ potential start questions for a route

See Trello card: [Make the ‘Add a question route’ button visible at all times](https://trello.com/c/itxN6e0h/866-routing-consider-making-the-add-a-question-route-button-visible-at-all-times-design)

<br>

#### How we’ll clarify what is / is not possible with simple routing

- We’ll add the sentence “You can only add one route from each question” to all versions of the ‘Add a question route’ start page
- We’ll show different versions of the routing start page depending on the criteria for routing that a user meets

See Trello card: [Hone existing content to clarify what is and is not possible with basic routing](https://trello.com/c/X3D9272a/870-routing-hone-existing-content-to-clarify-what-is-and-isnt-possible-with-basic-routing-the-rules) 

<br>

#### How we’ll clarify the difference between optional questions and routing

- We’ll change the wording used for the ‘Make this question optional’ checkbox. New wording will be “Make this question optional so people can leave it blank” (rather than “so people can skip it”)

See Trello card: [Help users differentiate between optional questions and routing](https://trello.com/c/xv3uVzLm/902-routing-help-users-differentiate-between-optional-questions-and-routing) 

<br>
<br>

## Why we’re doing this 

After an initial round of usability testing on simple routing (sprint 30), we decided to address any changes that were considered critical. 

It was important to balance the need for making changes to this feature with the need to move onto the next GOV.UK Forms feature as quickly as possible in order to meet our roadmap commitments.

We decided to prioritise these particular tasks because they were considered to be relatively ‘quick wins’ - meaning they should help form creators understand and add skip logic more easily but would not take up too much of the team’s resource.

<br>
<br>

## Key decisions 

### Make the ‘Add a question route’ button visible at all times 

Most users struggled to spot the ‘Add a question route’ button without prompting. They tended to look for a way to add routing within the ‘Add and edit your questions’ page or within the edit page of the particular question they wanted to skip.

Having a link or button to create a route within either of these pages was considered at the start of this feature, but was seen as being more complex and costly than the design that’s just been tested. There were also concerns about overloading the pages in question with more links/buttons, and how this might fit with future developments (such as multiple routes and branching) - hence the simpler, cheaper solution that’s just been tested.

In an attempt to improve the findability of the ‘Add a question route’ button by using another simpler, cheaper solution we decided to:

- make the ‘Add a route’ button available at all times
- create a new version of the routing start page with content that explains what form creators need to do if they try to add a route when their form doesn’t meet the criteria

The intention is that form creators will notice the ‘Add a question route’ button alongside the ‘Add a question’ button earlier on in their form creation journey. This will need to be tested at the next opportunity.

<br>

### Clarify what is / is not possible with simple routing

In testing, some users ran into issues because they weren’t clear what is and isn’t possible with routing. In particular, some users did not seem to realise that you can only create one route per question (meaning that ‘branching’ is not currently available). 

We already specify that you can only create a route from a ‘select from a list of options’ questions on the ‘Add a question route’ page. The existing wording is: “A route can only start from a question where people select one item from a list”. 

We also wondered how we might help form creators understand that it makes most sense to create a route for answers that need to skip a question, rather than the other way around. 

We wanted to look at where in the current content/journey we might be able to add some extra clarity around this.

Our main change was to update the content on the routing start page so that it explains more fully the criteria that a user needs to meet before adding a route. We did this by adding “You can only add one route from each question”.

We considered also adding content to help users understand that it makes most sense to create a route for answers that need to skip a question, rather than the other way around - possibly using an example. However, it was difficult to find appropriate wording without adding significant complexity to this page. We therefore decided to leave this for now and to monitor the need for this during future rounds of testing. 

<br>

### Clarify the difference between optional questions and routing 

In testing, some users chose to make the question to be skipped optional in an attempt to get around the ‘create a route’ task . In two cases they wrote hint text to explain this. (One chose to delete the question altogether.) Optional questions and routing could therefore be seen as the same thing by some users. We wondered how to make these more clearly defined so users could differentiate between them more easily. 

We’ve been using the word ‘skip’ in our optional question hint text, but not when describing routing. This seemed to conflate the two in the mind of at least one user.  

We decided to tweak the optional question hint text to remove the word ‘skip’ and use the term ‘leave blank’ instead. The new content says “Make this question optional so people can leave it blank”.

We decided that it’s not a priority to revisit the rest of the content/wording in any more depth at this point, but we’ll keep it on the radar for future testing and feedback.

<br>
<br>

## Designs

### ‘Add a route’ button now visible at all times 

The ‘Add a route’ button is now visible on the ‘Add and edit your questions’ page at all times - even if the criteria for adding a route are not met

![Add and edit your question screen with the grey ‘Add a question route’ button visible with a single question added. Screenshot](image.jpg)

<br>

### Question route start page - no criteria are met and no other route exists

New routing start page that form creators will see if they click the ‘Add a route’ button but do not yet meet any or all of the criteria for adding a route and no other routes exist.

A new sentence which says “You can only add one route from each question” is shown beneath the bullet points. (This sentence appears on all other variations of the routing start page too.)

![Add a question route screen with no radio options to start a route from. Screenshot](image.jpg)

...

<br>

### Question route start page - no criteria are met but other routes exist

New routing start page that form creators will see if they click ‘Add a route’ button when they do not meet the criteria for adding a route but at least one other route already exists

![Add a question route screen telling user “You have no more questions to start a route from”. Screenshot](image.jpg)

...

<br>

### Other versions of the routing start page - depending on how many potential start questions are available

![Three examples of the ‘Add a question route’ screen. Left, 1 available page, shows the screen with only one radio option available. Middle, 2 to 10 pages, shows the screen with three radio options. Right, 11+ pages, shows a select box component. Screenshot](image.jpg)

...

<br>

### New optional question wording - removing the word ‘skip’ and using ‘leave it blank’ instead for the checkbox label

![Question settings section of “Edit question” screen showing new version of checkbox label text. Screenshot](image.jpg)

<br>
___

<br>

[Back to the top](#simple-routing-v2)
