# Create long list autocomplete 

## Status 

Date created: *2024-11-26*  

## Contents

- [Create long list autocomplete](#create-long-list-autocomplete)
  - [Status](#status)
  - [Contents](#contents)
  - [What](#what)
    - [The problem](#the-problem)
    - [As-is](#as-is)
    - [To-be](#to-be)
  - [Key decisions](#key-decisions)
  - [Measuring impact](#measuring-impact)
  - [Designs](#designs)
    - [Iterated create a select from a list of options question journey](#iterated-create-a-select-from-a-list-of-options-question-journey)
    - [New step - How many options should people be able to select?](#new-step---how-many-options-should-people-be-able-to-select)
    - [Iterated Create a list of options page variations](#iterated-create-a-list-of-options-page-variations)
    - [New Enter your list's options into a text box page](#new-enter-your-lists-options-into-a-text-box-page)
    - [Iterated Edit question page - how we display answer settings and lists of options](#iterated-edit-question-page---how-we-display-answer-settings-and-lists-of-options)
    - [Edit selection type warning messages and flows](#edit-selection-type-warning-messages-and-flows)
    - [Error messages for entered options](#error-messages-for-entered-options)

___

## What

### The problem

- There a forms that require longer lists of options to select from and a lack of custom list creation is a barrier to onboarding more forms
- Form creators have to manually create long list questions
(up to 30 options)
- There is no quick way to create list of options
- Long lists of options are not user friendly for form fillers
- We don't have autocomplete support for long lists


### As-is

- Form creator creates a question where the answer can be selected from a list of options. The list of options is limited to 30. Form creator can set if a person can select only one option or one or more options.
- Form creator uses single repeatable fields to create their list of options
- Form creator can specify if the list should include 'none of the above'

### To-be


## Key decisions

- For select only one option we will allow long list for up to 1000 options. When the list of options is longer than 30, we present it to the form fillers as an autocomplete field. Form fillers will be able to search and find the options by typing into an autocomplete box. When the list of options is 30 and under we present it as radios.
- For select one or more (checkboxes) we keep the limit to 30 options, so to ensure that form fillers have a positive user experience, as long lists can be difficult to use.
- We introduce a new step where form creators can choose how many options should people be able to select, so that we can tailor their journey for creating lists of options
- We introduce an additional way of entering options. Form creators can enter all the options into one text box with each option on a new line
- After form creator has made their list of options, on the Edit page we present the list of options as a bullet list and we play back the amount of options they created for reassurance. If the list is longer than 10 options we present it in a 'detail' component, so that

## Measuring impact

<br>

## Designs

### Iterated create a select from a list of options question journey

### New step - How many options should people be able to select?

### Iterated Create a list of options page variations 

### New Enter your list's options into a text box page

### Iterated Edit question page - how we display answer settings and lists of options

### Edit selection type warning messages and flows

### Error messages for entered options

