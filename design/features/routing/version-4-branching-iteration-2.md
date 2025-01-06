# Branching and exit pages iteration 2

Date created: 2024-11-14

* * *

## Contents

- [What this documentation covers](#what-this-documentation-covers)
- [Research summary](#research-summary)
- [Designs](#designs)

* * *

## What this documentation covers

This is the second iteration of designs for adding branching functionality to the product. It covers minor updates to the design and content of the 1st iteration, based on findings from user research.

[This iteration’s designs in Mural](https://app.mural.co/t/gaap0347/m/gaap0347/1728478914347/6a7e0b709f50f00f81cab37414fdf44ec8601a70?wid=0-1732104447782).

## Research summary

We shared our initial designs with 4 participants to get some initial feedback in late November 2024. We aimed to find out:

- where and how they’d expect to add routes, branches and exit pages
- how they understood the designs 
- what things in the designs were confusing or unclear

### Findings and issues to address

[Research findings Mural](https://app.mural.co/t/gaap0347/m/gaap0347/1727432983705/a5f21ac1a04ec2831cda45dd723328346546891f?sender=u12d19b597a88e8b64fc22126)

The main things we decided to address were: 

- the initial guidance about what you can and can’t do with routes could be clearer - especially in relation to ‘branches’
- there was some confusion about the ‘Edit question x’s routes’ page - and people were easily missing the link to ‘set more questions to skip’
- the ‘Set questions to skip’ page was not easily understood and it took some time for people to figure out what it meant and what they needed to do
- there was a bit of confusion caused by the labelling of routes in the question list page

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

### Route 2: set questions to skip

<img src="/design/features/routing/screenshots-v4/set-questions-to-skip-page.png" width="500">

#### Description of the image and the changes made in this iteration: 

This page plays back the initial question and route 2 so far - the route people take if they don’t select the answer that takes them down route 1. It then asks you to select questions to skip these people from and to - allowing you to create 2 branches of questions. The page also includes some guidance in a details component and a green ‘save and continue’ button. 

The H1 is now ‘Route 2: set questions to skip’. This has changed from ‘Set questions to skip’ to make it more specific and to highlight what route this relates to. 

We then playback route 2 so far. In this example this reads: 

> If the answer to: Have you had a BPSS check?
> 
> is not: Yes
> 
> continue to: 3. What are the company details? 

We’ve added the playback of this information to this page to make it clear which route the form creator is editing and what the people on the route will have answered so far. This replaces the guidance that was shown here previously. The guidance has been moved into a details component. 

Then there are two select components for the form creator to set the questions to skip from and to. The labels and default select option text read: 

> Then after the person answers
>
> Select a question
>
> take them to
>
> Select a question or page

There is then an expandable details component. 

The link text is: Why set questions to skip?

The guidance in the details component is: 

> People who select an answer that does not have a route assigned to it will continue to the next question.
>
> If you need to, you can make these people skip one or more questions later in the form. For example, you might want them to skip route 1’s questions. This allows you to create 2 different ‘branches’ of questions.

This guidance has been updated to make it clearer what’s happening on this page, what you can do on it, and why. 

This is followed by a green ‘Save and continue’ button and a ‘Cancel’ link.

#### Validation and error messages for this page: 

First input not answered: 
> Select the question you want to skip from

Second input not answered: 
> Select the question or page you want to take the person to

First question is after the destination question: 
> The question you want to skip from must be before the question you want to take the person to

First question and destination question are the same: 
> The question you want to skip from cannot be the same question you want to take them to

First question and destination question are consecutive already: 
> The question you want to skip to is already straight after the question you want to skip from

### Question x’s routes - with Routes 1 and 2 set

<img src="/design/features/routing/screenshots-v4/questions-xs-routes-with-2-routes.png" width="500">

#### Description of the image and the changes made in this iteration: 

People are returned to this page after setting questions to skip for Route 2. The page now shows the question that will be skipped as part of Route 2, as well as the option to edit or delete Route 2. 

The H1 is ‘Questions 2’s routes’. 

The page then plays back the question the routes in the page apply to. In this example: 
> Question 2: Are you directly employed? 

There are then 2 grey boxes - using the ‘summary card’ component. The first is titled ‘Route 1’ and the second ‘Route 2’.

The Route 1 box is unchanged from previously. It reads: 
> If the answer is: Yes
> 
> take the person to: 4. What is your business area? 

There is also a blue ‘Edit’ link in the top right corner of the Route 1 summary card. 

In the Route 2 summary card, we then play back Route 2. It reads: 
> For any other answer, continue to: 3. What are your company details? 
> 
> Then after the person answers: 3. What are the company details? 
> 
> take them to: 6. Your personal details

There is then a red ‘Delete routes’ button. And a link to ‘Continue to your questions’. 

### Add and edit your questions - showing routes

<img src="/design/features/routing/screenshots-v4/add-and-edit-your-questions-page-with-routes.png" width="500">

#### Description of the image and the changes made in this iteration: 

This page shows a list of the questions in a form. It shows what number each question is and its question text. To the right of each question there’s a ‘Edit’ link, ‘Move up’ and ‘Move down’ grey buttons. Between 3 of the questions in the design there are route descriptions to explain to the form creator what routing has been set and where people are skipped to. 

In this iteration, the wording for the label of a route has been made more specific. And the wording of the description of a route has been made more concise. 

There are 3 examples in the image. The route label and description between questions 1 and 2 reads: 
> Route 1 of question 1’s routes
> If “Have you undergone a BPSS check?” is answered as “No” go to the exit page, “You are not eligible for this service”

The route label and description between questions 2 and 3 reads: 
> Route 1 of question 2’s routes
> If “Are you directly employed?” is answered as “Yes” go to 4, “What is your business area?”

The route label and description between questions 3 and 4 reads: 
> Route 2 of question 2’s routes
> After 3, “What are the company details?” go to 6, “Your personal details”

Each route description also has a blue ‘Edit’ link to the right. 

### Your questions - read-only view of a live form

<img src="/design/features/routing/screenshots-v4/your-questions-page-for-a-live-form-with-routes.png" width="500">

#### Description of the image and the changes made in this iteration: 

This page shows the list of a live form’s questions. It lists each of the form’s questions in a summary card component. If a route starts from a question, the summary card for that question also includes a description of that route. The image shows examples of 3 questions with routes.

The summary card for Question 1 reads: 
> 1\. Have you undergone a BPSS check?
> 
> Answer type: Selection from a list, one option only.
> 
> Options: Yes, No
>
> Route: If the answer is “No” go to the exit page, “You are not eligible for this service”

The summary card for Question 2 reads: 
> 2\. Are you directly employed?
> 
> Answer type: Selection from a list, one option only
> 
> Options: Yes, No
> 
> Route: If the answer is “Yes” go to 4, “What is your business area?”

The summary card for Question 3 reads: 
> 3\. What are the company details?
> 
> Answer type
>
> Route: More than a single line of text
>
> Go to 6, “Your personal details”
