# Routing 

## Status 

Date updated: *2024-10-31*  

## Contents

- [Branching and exit pages](#branching-and-exit-pages-iteration-1)
  - [What is branching and exit pages](#what-is-branching-and-exit-pages)
    - [Branching and exit pages user stories](#branching-and-exit-pages-user-stories)
  - [Why are we introducing branching and exit pages](#why-are-we-introducing-branching-and-exit-pages)
    - [Branching and exit pages hypotheses](#branching-and-exit-pages-hypotheses)

- [Simple routing logic (skip questions)](#simple-routing-logic-skip-questions)
  - [What is simple routing ](#what-is-simple-routing)
    - [Simple routing user stories](#simple-routing-user-stories)
  - [Why are we adding simple routing ](#why-are-we-adding-simple-routing)
    - [Simple routing hypothesis](#simple-routing-hypothesis)

___

## Branching and exit pages (iteration 1)

Date updated: *2024-10-24* 

- Epic trello card: https://trello.com/c/a5c3JaWu/1908-epic-branching-and-exit-pages  
- Mural working board: https://app.mural.co/t/gaap0347/m/gaap0347/1728478914347/6a7e0b709f50f00f81cab37414fdf44ec8601a70?wid=0-1729257264973  
- Routing and branching terminology (how we decided what to deliver): https://docs.google.com/document/d/1lXKKGyT6kbFc0EbthTPiEHK5sEIc1EuVqSLXuQ1MXPc/edit?usp=sharing  

<br>  

### What are branching and exit pages  

This feature introduces additional functionality to the form building tool to allow form creators to add secondary skip logic to a later question. This creates two unique branches that form fillers can go down. 

As before, you can skip someone to a later question in a form based on their response to a question where they have to select one answer from a list. But while people who select any other answer will still continue to the next question, you can now make them skip one or more questions later in the form. You can also direct them to a page that lets them exit the form, for example if they're not eligible.

#### Branching and exit pages user stories

**As a form creator**, I need to ask users the questions that are relevant to them based on the previous answers they’ve given, so we only collect the data we need.    

**As a form filler**, I need to only see questions that are relevant to me so that I can complete the form easily.  

**As a form processor**, I need to see the information relevant to each user in a way that I can easily transfer/paste it to where it needs to be saved, so that I don’t have to waste time manually fixing the data.  

<br>  

### Why are we introducing branching and exit pages?

When users fill in forms they can currently be skipped over certain questions, based on a previous answer. This has helped reduce the number of questions a form filler might need to fill in or see that weren’t relevant to them or their task. However, it means that form creators are currently forced to create ‘check questions’ that they can then use to skip people over more questions.  

This can add more complexity to a form for both form creators and form fillers, as the ‘check questions’ need to be clear and correctly located within the form journey to make sure form fillers are not asked for information they might not have or cannot understand. The latter can cause anxiety for people completing forms and can add to cognitive load. It can also be a waste of their time, and lead to incorrect information being supplied.  

#### Branching and exit pages hypotheses

We believe that by offering one branch from a question, based on the ‘selection from a list’ answer type, we can help form creators create better forms that only ask for information that processing teams need to action a submission. 

We believe that by offering one ‘exit page’ from a question, based on the ‘selection from a list’ answer type, we can help form creators direct form fillers to the information that’s most relevant to them - without filling in a form they’re not eligible for. This will save them time and effort.  

[Back to the top](#routing)

___

## Simple routing logic (skip questions)

Date created: *2023-05-23*  

- Epic trello card: https://trello.com/c/nBnFZQlw/135-epic-simple-routing  
- Mural working board: https://app.mural.co/invitation/mural/gaap0347/1671196865223?sender=ue1ef9fc3c2ad3697c3c93132&key=09616cf9-ae28-43a7-8810-10970a59a765  
- Basic routing feature write up: https://docs.google.com/document/d/1i7T5D3PQw4hB1wgISi-r5086Fzw1-3nKnwaCGbNMi1E/edit#heading=h.h2rnqdwxl250  

<br>  

### What is simple routing?   

This feature introduces new functionality to the form building tool to help form creators create simple skip logic for questions. This means you can skip someone to a later question in a form based on their response to a question where they have to select one answer from a list.

#### Simple routing user stories

**As a form creator**, I need to allow users to skip a question based on their previous answer, so that we only collect the information needed.

**As a form filler**, I need to skip a question based on my previous answer, so that I don't have to give more information than I need to.

<br>  

### Why are we adding simple routing? 

When users fill in forms they’re currently shown all the questions within a form: this means they’re potentially presented with questions that are not relevant to their submission. This can cause anxiety for people completing forms as they may not have the information needed or they may not understand what they’re being asked for. It can also be a waste of their time and add to cognitive load.  

When creating paper forms, we know that form creators use wording to tell the form filler when a piece of information is needed or if they should go to a later section or question to continue.  

We also know that paper forms can be completed in any order, with information being skipped if the person filling in the form does not have the information or does not feel that a certain question applies to them. This can result in incomplete forms being submitted.  

Without skip functionality in an HTML form users are forced to go through all the questions even when they’re not relevant to their submission. We originally implemented a feature to allow form creators to make questions ‘optional’, meaning the person completing a form can pass over questions they do not need to complete. However, this means form fillers have to decide whether they think a question is relevant to them, and they may decide not to answer when in fact they need to. It also means that form creators may feel the need to clarify who should answer the question in the 'hint text', which may or may not be read by the form completer.  


#### Simple routing hypothesis  

We believe that by offering simple skip logic, based on the ‘selection from a list’ answer type, we can help form creators create better forms that only ask for information that the processing team need to action a submission.  

[Back to the top](#routing)

___
