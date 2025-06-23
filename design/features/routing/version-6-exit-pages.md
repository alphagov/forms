# Exit pages iteration 2

Date created: 2025-06-20

* * *

## Contents

- [What this documentation covers](#what-this-documentation-covers)
- [Designs](#designs)

* * *

## What this documentation covers

This is based on the first iteration that was created with minor changes that were then put live in production. 

[This iteration’s designs in Mural](https://app.mural.co/t/gaap0347/m/gaap0347/1740496027781/5a34f1bab377b7c7126742591825b0d3d616b9dc?wid=0-1740496156549).

## Designs

### Add a route from a question

<img alt="Page titled “Add a route from a question” with guidance and radio options. Screenshot" src="screenshots-v6/001-add-a-route-from-a-question-withOptions.png" width="500">

#### Description of the image and the changes made in this iteration: 

The page’s H1 is ‘Add a route from a question’. It then has some guidance and a radio question for form creators to select a question to start a route from.

The guidance aims to set expectations for the form creator about what they can and cannot do with routing. It has been updated since the last iteration to make it clearer. It now reads: 

> You can add a route to a question so if someone selects one specific answer, they’ll be skipped to:  
>  
> - a later question  
> - the end of the form  
> - an ‘exit page’ to remove them from the form - for example, because they’re not eligible  
>  
> People who select any other answer will continue to the next question and through the rest of the form.  

Note: this implementation did not include exit page functionality and so missed additional guidance content that was added later. 

The guidance is followed by a question:  

> Which question do you want to start a route from?  

Then hint text:  

> A route can only start from a question where people select one item from a list.  

The answer options are all the ‘selection from a list’ questions from the form that only allow one answer (radio questions). In the example in the image above, there are 2 questions the form creator can select from. 

Finally, there’s a green ‘Continue’ button.

After the form creator has selected a question to start their route from and then ‘Continue’, they move to the ‘Edit route 1’ page.

### Add route 1: select an answer and where to skip to - showing ‘skip the person to’ dropdown  

<img src="screenshots-v6/002-add-route-1-skipPersonTo-Dropdown.png" width="500">

#### Description of the image and the changes made in this iteration: 

The page’s H1 is ‘Add route 1: select an answer and where to skip to’. It then has some guidance before a summary component showing the question number and content. In this example it reads: 

> Question 2: Have you had a BPSS check?  

The guidance above aims to set expectations for the form creator about what they can do with content of the current and following questions. It reads: 

> You can skip people who select one specific answer to [question 2] to a later question or page. People who select any other answer will continue to [question 3].

Next are two dropdowns that the form creator select from to create their route. The first, ‘If the answer selected is’, has already been selected and is showing the word ‘No’. The second dropdown labelled ‘skip the person to’ is covered by an open dropdown menu showing the list of options available to the form creator. It lists the placeholder text, ‘Select a question or page’, followed by all of the questions, number followed by content, left in the form starting from the current question. The final two rows of the dropdown list give the form creator the option to see and create a new ‘exit page’ for the above answer. They show: 

> An ‘exxit page’ to leave the form  
>   Add an exit page  

By selecting the ‘Add an exit page’ option from the list when the form creator clicks ‘Save and continue’ they are taken to the ‘Edit exit page’ screen.

