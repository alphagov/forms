# Branching iteration 3

Date created: 2025-06-11

* * *

## Contents

- [What this documentation covers](#what-this-documentation-covers)
- [Research summary](#research-summary)
- [Designs](#designs)

* * *

## What this documentation covers

This is the third iteration that was created and put live into production based on previous research. 

[This iteration’s designs in Mural](https://app.mural.co/t/gaap0347/m/gaap0347/1728478914347/6a7e0b709f50f00f81cab37414fdf44ec8601a70?wid=0-1737023334487).

## Designs

### Add a route from a question

<img alt="Page titled “Add a route from a question” with guidance and radio options, “Which question do you want to add a route from?”. Screenshot" src="screenshots-v5/001-add-a-route-from-a-question-withOptions.png" width="500">
<img alt="There is a problem: Select the question you want to add a route from" src="screenshots-v5/001-add-a-route-from-a-question-error.png" width="300">

#### Description of the image and the changes made in this iteration: 

The page’s H1 is ‘Add a route from a question’. It then has some guidance and a radio question for form creators to select a question to start a route from.

The guidance aims to set expectations for the form creator about what they can and cannot do with routing. It has been updated since the last iteration to make it clearer. It now reads: 

> You can add a route from a question where people can select only one answer from a list.  
>   
> If someone selects the answer you specify, they’ll skip forward to a later question, or the end of the form.  
>   
> People who select any other answer will continue to the next question. If you need to, you can add a second route so they skip one or more questions later in the form.
>
> You can only add a route from a question that does not already have 2 routes. Go back to your questions if you need to edit an existing route.  

Note: this implementation did not include exit page functionality and so missed additional guidance content that was added later. 

The guidance is followed by a question: 

> Which question do you want to add a route from? 

This was previously followed by hint text but has been incorporated into the guidance removing the need for it as part of the question component.  

The answer options are all the ‘selection from a list’ questions from the form that only allow one answer (radio questions). In the example in the image above, there are 2 questions the form creator can select from. 

Finally, there’s a green ‘Continue’ button.

After the form creator has selected a question to start their route from and then ‘Continue’, they move to the ‘Edit route 1’ page.

### Add a route from a question - You cannot add a route yet

<img alt="Page titled “Add a route from a question” with guidance the bottom section has been replaced by new static content “You cannot add a route yet” with more context beneath. Screenshot" src="screenshots-v5/002-add-a-route-from-a-question-YouCannotAddARouteYet.png" width="500">

#### Description of the image and the changes made in this iteration: 

This page shows an alternative version of the ‘Add a route from a question’ page where a form does not meet the minimum criteria that allows routing to be added. 

The page heading and guidance content remain the same while the bottom section is replaced by a section titled ‘You cannot add a route yet’. The content reads:  

> Before you can add a route, your form needs to have a question that:  
>   
> - asks people to select only one option from a list  
> - has at least one question after it  
>   
> It’s usually easiest to create all your form’s questions first, then add the routes you need.

The updated content reflects more accurately the criteria required to be able to add routing to a question. We also add new additional context of adding all your forms questions before adding your routing. 

The page ends with a blue ‘Back to your questions’ link. 

### Add a route from a question - You have no more questions to add a route from

<img alt="Page titled “Add a route from a question” with guidance the bottom section has been replaced by new static content “You have no more questions to add a route from” with more context beneath. Screenshot" src="screenshots-v5/002-add-a-route-from-a-question-YouHaveNoMoreQuestionsToAddARouteFrom.png" width="500">

#### Description of the image and the changes made in this iteration: 

This page shows an alternative version of the ‘Add a route from a question’ page where a form may already have routing applied to all possible questions that meet the minimum criteria meaning there are no longer any questions that can have new routes added. 

The page heading and guidance content remain the same while the bottom section is replaced by a section titled ‘You have no more questions to add a route from’. The content reads:  

> You can only add a route from a question that does not already have 2 routes. If you need to edit an existing route, go back to your questions.  

The new content more accurately reflects the updated criteria for routing and informs form creators to consider returning to their question list if they need to make changes to an existing question’s routes. 

The page ends with a blue ‘Back to your questions’ link. 

### Edit route 1

We’ve made no changes to this page in this iteration. The form creator selects the answer that will skip people forward, and the question they want them to skip to. 

When they click ‘Continue’ they are taken to the ‘Question x’s routes’ page.

### Question x’s routes - with Route 1 set

<img alt="Page titled “Question 2’s routes” showing the question text and a summary card for ‘route 1’. Row 1 of the summary card shows “If the answer is Yes”, with the second row “take the person to 4. What is your business area?”. Below is explanatory text for ‘any other answer’. Screenshot" src="screenshots-v5/003-question-xs-routes-route1Set.png" width="500">

#### Description of the image and the changes made in this iteration: 

This page shows the routes that you have from a specific question. It also allows you to:

- edit the first route  
- delete the first route  
- set questions to skip later in the form for any other answer    
- delete all routes from this question, after having added 2 routes to the question   
- continue to your questions  

The H1 is now ‘Questions 2’s routes’. This was changed from ‘Edit question 2’s routes’ for accuracy - because you can’t actually edit the routes on this page.

The page then plays back the question the routes in the page apply to. In this example: 

> Question 2: Are you directly employed? 

There is then 1 grey box - using the ‘summary card’ component. Titled ‘Route 1’.

There is a blue ‘Edit’ link alongside a newly added ‘Delete’ link in the top right corner of the Route 1 summary card. 

The Route 1 box content has not been updated in this iteration. It shows the route that has been created by the form creator. It reads: 

> If the answer is: Yes
> 
> take the person to: 4. What is your business area? 

Below the Route 1 box is now a secondary heading, ‘Any other answer’, followed by guidance content explaining how the forms routes will normally work for people filling in the form who haven’t selected the answer that triggers Route 1. This content reads:  

> People who select any other answer will continue to question 3.  
>  
> If you need to, you can make these people skip one or more questions later in the form. For example, you might want them to skip route 1’s questions to create 2 different ‘branches’ of questions.

Next is a grey secondary action button ‘Set questions to skip’.  

This has changed from the previous version to try to make it clearer how the other routes work and that the form creator can change the default form flow for the other routes on this screen by way of the button.

We have then hidden the previously always there red ‘Delete routes’ button to reduce confusion. Finally there is a link to ‘Continue to your questions’. 

If the form creator selects the button to ‘Set questions to skip’ they’ll go to the ‘Set questions to skip’ page.  

### Set questions to skip

We’ve made no changes to this page in this iteration. The form creator selects the question that will people will skip from if they haven’t triggered Route 1, and the question they want them to skip to after answer the question. 

When they click ‘Save and continue’ they are taken back to the ‘Question x’s routes’ page.

### Question x’s routes - with Route 1 and Route for any other answer set

<img alt="Page titled “Question 2’s routes” now showing two summary cards. Route 1 and Route for any other answer. Screenshot" src="screenshots-v5/003-question-xs-routes-bothRoutesSet.png" width="500">

#### Description of the image and the changes made in this iteration: 

People are returned to this page after setting questions to skip for Route 2. The page now shows the question that will be skipped as part of Route for any other answer, as well as the option to edit or delete Route for any other answer.

The H1 is ‘Questions 2’s routes’.

The page then plays back the question the routes in the page apply to. In this example:  

> Question 2: Are you directly employed? 

There are then 2 grey boxes - using the ‘summary card’ component. The first is titled ‘Route 1’ and the second ‘Route for any other answer’.

The Route 1 box is unchanged from previously. It reads:

> If the answer is: Yes
> 
> take the person to: 4. What is your business area?

There are also blue ‘Edit’ and ‘Delete’ links in the top right corner of the Route 1 summary card.

In the Route for any other answer summary card, we then play back the secondary route associated with this question. It reads:

> For any other answer, continue to: 3. What are your company details?  
>  
> Then after the person answers: 3. What are the company details?  
>  
> take them to: 6. Your personal details  

There is then a red ‘Delete routes’ button. And a link to ‘Continue to your questions’.
