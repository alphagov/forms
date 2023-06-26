# Simple routing logic

## Status

Date created: *2023-05-23*  

Epic trello card: https://trello.com/c/nBnFZQlw/135-epic-simple-routing  
Mural working board: https://app.mural.co/invitation/mural/gaap0347/1671196865223?sender=ue1ef9fc3c2ad3697c3c93132&key=09616cf9-ae28-43a7-8810-10970a59a765  
Basic routing feature write up: https://docs.google.com/document/d/1i7T5D3PQw4hB1wgISi-r5086Fzw1-3nKnwaCGbNMi1E/edit#heading=h.h2rnqdwxl250  
___

## Contents

- [Simple routing logic](#simple-routing-logic)
  - [Status](#status)
  - [Contents](#contents)
  - [What](#what)
  - [Why](#why)

___

<br>

## What

This feature is introduces functionality within the form building tool to help form creators create simple skip logic for questions, meaning people completing a form should only be asked relevant questions based on a previously given answer.

### User stories

**As a form creator**, I need to allow users to skip a question based on their previous answer, so that we only collect the information needed.

**As a form filler**, I need to skip a question based on my previous answer, so that I don't have to give more information than I need to.

<br>

## Why

When users fill in forms they are currently shown all the questions within a form, meaning they are potentially presented with questions that are not relevant to their submission. This can cause people completing forms anxiety when filling them in, as they may not have the information required or may not understand what they are being asked for.  

We know when creating paper forms, creators use language to inform the form filler of when a piece of information is required or if they should go to a later section or question to continue.  

We also know that paper forms can be completed in any order with information being skipped if the person filling in the form doesn’t have the information or doesn’t feel like a certain question doesn’t apply to them and their submission. This can result in incomplete forms being submitted.  

Without skip functionality being part of an HTML form users are forced to go through all the questions even when they are not relevant to their submissions success. We originally implemented a feature to allow form creators to make questions “optional”, meaning the person completing a form can pass over questions they do not need to complete. However, this means form fillers have to decide whether they think a question is relevant to them, and they may decide not to answer when in fact they need to. It also means that form creators may feel the need to clarify who should answer the question in the 'hint text', which may or may not be read by the form completer.

## Hypothesis

**We believe** by offering simple skip logic, based on the “selection from a list” answer type, we can help form creators create better forms that only ask for information that the processing team require to action a submission.  

<br>

___

<br>

[Back to the top](#simple-routing-logic)
