# Simple routing v1

## Status

Date created: *2023-05-25*  

Developed  

___

## Contents

- [Feature name](#feature-name)
  - [Status](#status)
  - [Contents](#contents)
  - [What](#what)
  - [Designs](#designs)

___

<br>

## What

### As-is

- form creator creates questions and marks them as optional giving content as part of hint text to explain who needs complete a question

### To-be

- from creator can select radio option and set a page to go to if selected. If a radio option has no set page then option will go to next page in the order (unless another option has the next page set as the next step)  
- form creator HAS to select a next question for each radio option IF one radio option in a list has had a next question set  
- form creator can set next (single) question as skippable if radio option X is chosen  

## Designs

### New “Add a question route” journey and view on questions list page

![Add and edit your questions page with new grey “Add a question route” button next to the green “Add a question” button. Screenshot.](https://github.com/alphagov/forms/assets/35372982/700ad8f7-0fa7-4484-b636-2263beb141d2)
*As part of the list of questions added to the form there is a new row, with the row heading “Question 2’s route”. To the right are the starting question, the answer to base the route on and the page to take the user to if the answer is chosen. There is an edit link at the end of the row.*

### Adding a new route 

![Simple routing exploration - 2022-12-16_2023-05-25_08-12-01](https://github.com/alphagov/forms/assets/35372982/3b72e7a3-8e41-43fb-86eb-9e09928bfce1)
*caption2*

### Editing an existing route

![Simple routing exploration - 2022-12-16_2023-05-25_08-12-56](https://github.com/alphagov/forms/assets/35372982/4af90739-72ce-4ef3-b110-ff1c041f6e3e)
*caption3*

### Breaking changes errors

![Simple routing exploration - 2022-12-16_2023-05-25_08-20-54](https://github.com/alphagov/forms/assets/35372982/c9d01a5c-48d9-4abf-816f-a22de683a665)
*caption4*


<br>

___

<br>

[Back to the top](#simple-routing-v1)
