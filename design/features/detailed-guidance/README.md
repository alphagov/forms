# Add guidance to help people answer the question ('detailed guidance')

## Status

Date created: *2023-10-03*  

Epic trello card: https://trello.com/c/HfVi4JrB/818-add-detailed-guidance-to-questions  
Mural working board: https://app.mural.co/t/gaap0347/m/gaap0347/1683038152877/e16c675d20fcbc7595d016d03eeb5d7024fe0020?sender=ue1ef9fc3c2ad3697c3c93132  
___

## Contents

- [Add guidance to help people answer the question (detailed guidance)](#add-guidance-to-help-people-answer-the-question-detailed-guidance)
  - [Status](#status)
  - [Contents](#contents)
  - [What](#what)
  - [Why](#why)
  - [Hypothesis](#hypothesis)

___

<br>

## What

This feature introduces new functionality to the form building tool to allow form creators to add more complex help text to a question page. This 'guidance' text will appear above the question, on the same page.  

This is considered the best way to introduce complex information when most (if not all) form completers will need to read that information in order to complete a single question.  

Where only a minority of users need additional guidance, a separate feature will need to be explored and considered, such as a details component (show / hide).  

Where a complex piece of guidance or instructions are needed before a section or group of questions (rather than a single question) this will need to be considered as part of yet another future feature, such as an interstitial page.

### User stories

**As a form creator**, I need to add content before a question, so that the user has any context that they need to answer that question.

**As a form completer**, I need to understand how to answer a question, so that I feel confident about my answer and don’t need to go looking for help.

<br>

## Why

Currently, when form creators create questions they're often using quite long question text, along with hint text, to explain the information that's required from the form completers. 

We've also seen form creators try to insert links to relevant guidance pages or reference documents as part of the hint text in order to help their users complete their form effectively.  

Because of the way question text, hint text and inputs are associated using the design system components, and the way in which the page displays and reacts with assistive technology, this is not an accessible implementation.

There is, however, a pattern within the design system which looks at more complex questions that require additional information. This helps explain to form completers how to complete a specific question at the time of need, while answering the question in the form.  

## Hypothesis

We believe that by offering the ability to add more complex information - including formatting - before a question, form creators will be able to direct form completers to any relevant information and provide the level of contextual detail they need to answer a difficult question.  

We believe this offering will improve the data being collected, improve processing times, and help form completers to get to the outcome they need.  

<br>

___

<br>

[Back to the top](#add-guidance-to-help-people-answer-the-question-detailed-guidance)
