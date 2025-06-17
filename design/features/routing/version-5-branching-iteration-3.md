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

<img src="/design/features/routing/screenshots-v4/add-a-route-from-a-question.png" width="500">

#### Description of the image and the changes made in this iteration: 

The page’s H1 is ‘Add a route from a question’. It then has some guidance and a radio question for form creators to select a question to start a route from.

The guidance aims to set expectations for the form creator about what they can and cannot do with routing. It has been updated since the last iteration to make it clearer. It now reads: 

> You can set up a route so if someone selects a specific answer to a question they’ll skip forward to a later question, or the end of the form.
> 
> People who select any other answer will continue to the next question. If you need to, you can make them skip one or more questions later in the form.
> 
> Or you can take someone who selects a specific answer to an ‘exit page’ to remove them from the form. For example, because they’re not eligible.

Note: the last paragraph will be hidden until we implement exit page functionality. 

The guidance is followed by a question: 

> Which question do you want to start a route from? 

Then hint text:

> A route can only start from a question where people select one item from a list.

The answer options are all the ‘selection from a list’ questions from the form that only allow one answer (radio questions). In the example in the image above, there are 2 questions the form creator can select from. 

Finally, there’s a green ‘Continue’ button.

After the form creator has selected a question to start their route from and then ‘Continue’, they move to the ‘Edit route 1’ page.

### Edit route 1

We’ve made no changes to this page in this iteration. The form creator selects the answer that will skip people forward, and the question they want them to skip to. 

When they click ‘Continue’ they are taken to the ‘Question x’s routes’ page.

### Question x’s routes - with Route 1 set

<img src="/design/features/routing/screenshots-v4/question-xs-routes-with-1-route.png" width="500">

#### Description of the image and the changes made in this iteration: 

This page shows the routes that you have from a specific question. It also allows you to:

- edit the first route
- set questions to skip later in the form for route 2
- delete all routes from this question
- continue to your questions

The H1 is now ‘Questions 2’s routes’. This was changed from ‘Edit question 2’s routes’ for accuracy - because you can’t actually edit the routes on this page.

The page then plays back the question the routes in the page apply to. In this example: 

> Question 2: Are you directly employed? 

There are then 2 grey boxes - using the ‘summary card’ component. The first is titled ‘Route 1’ and the second ‘Route 2’.

The Route 1 box is unchanged from the previous iteration. It shows the route that has been created by the form creator. It reads: 

> If the answer is: Yes
> 
> take the person to: 4. What is your business area? 

There is also a blue ‘Edit’ link in the top right corner of the Route 1 summary card. 

The Route 2 box was previously titled ‘For any other answer’. The title has been changed to ‘Route 2’ so that this route can be more easily referred to on this page and in other places. And because otherwise it didn’t really make sense to number Route 1. 

In the Route 2 summary card, we then play back what Route 2 is so far with a link to set questions to skip later in the form. It reads: 

> For any other answer, continue to: 3. What are your company details? 
> 
> Then: Set one or more questions to skip later in the form (optional)

This has also changed from the previous version to try to make it clearer what is happening in Route 2 and that you can add questions to skip if you need to.

There is then a red ‘Delete routes’ button. And a link to ‘Continue to your questions’. 

If the form creator selects the link to ‘set more questions’ to skip they’ll go to the ‘Route 2: set questions to skip’ page.
