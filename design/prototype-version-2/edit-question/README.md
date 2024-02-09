# Edit question page

## Context

For this round there we made a large change to the level of information we gave form creators for each of the options when creating their form questions. This included more useful hint text and more explicit input labels.  

As part of the testing we asked users to create a form exploring how they experienced the iterated version of adding a short answer and date question type. We also tested how they previewed a question.  
We then set the task of asking the participant to update an existing form, making changes based on feedback from a colleague.  

## What we tested last time

![Old version of edit page 1. Screenshot](../../prototype-version-1/screenshots/006-Edit-question-1-hint-open.png)
*Page with “Page 1” caption above heading “Edit page”.*

A secondary heading, “Question”, comes directly before the hint text “Long version - for example, What is your name?” and a text input.  
A second hint text of “Short version - for example, Name” comes next before a second text input.

Below is another secondary heading, “Answer”, with the hint text “What kind of answer you need to this question”. There are then radio buttons that determine the input type required:

- A single line of text
- An email address
- An address
- A phone number
- A National Insurance number
- A date

There is a detail component, blue link with an arrow before the text, “Add hint text”, that is expanded revealing the hint text “A short hint to help people answer the question” before a text input.

The page ends with a green “Save and create next page” button; a red “Delete page” button; the word ‘or’; and finally a “go to page list” link.

<!-- describe side preview pane -->
On the right side of the screen there is a grey “Update preview” button above an “Open in a new tab” link.

Below the link is a smaller version of an empty GOV.UK service page within an iframe, mimicking a mobile screen. It shows the GOV.UK logo on a black header. Within the body of the page is a ‘Back’ link and below this is a green ‘Continue’ button.  


### What we saw  

- All users were unsure what a ‘short’ and ‘long’ version question was and why they would need to have or use both, this caused some hesitation  
  > P3: “It’s an unexpected question I guess”  
- 2 users questioned what the ‘answer’ options were doing. 1 guessed that it would check format of the answers from people filling in the form. The other questioned if that was what was happening as they were unsure  
  > P2: “I like that it gives these options here (answer types) I don’t know how that will change the formatting when people are asked these questions. If I say date will it come up with boxes? Is that what this does? Does it change the format?”  
- When asked 2 users commented about potentially missing ‘answer’ types. Both suggesting the need for multiple lines of text, or “free text” boxes. 1 also suggesting an ‘answer’ type option for ‘name’  
  > P3: “I would call it ‘free text’, we have had answers like that, not sure ‘multiple lines’ is common language”   
  > P1: “...you might want Name as a type here too. If you wanted first name and last name separately. At the moment you’d have to do two separate form fields.”  
- All users were able to use the hint text feature to add content about the reference number and expected format, but 1 user mentioned they wanted a numerical field rather than an open text field so they could restrict what was entered  
  > P1: “Here I’m being forced into using a single line of text”    
- None of the users naturally noticed the preview pane on the right of the screen. When asked about it   
  - users were unsure what it was, until they came back to edit an existing question     
  - 1 user expected it to auto populate with questions as they built their form    
    > P1: “When you’re creating things on Whitehall, preview isn’t always a preview. [It doesn’t actually show you how it’s going to look] So that’s maybe shifted my mistrust of preview buttons.”    
    > P2: “If they [previews of each question] could all be there at once it would be a lot quicker.”      

## What we changed and why

- Improved the content for the ‘question’ input labels - adding a label specific to the ‘short version’ of the question  
- Added new hint text for each ‘question’ input to help guide the user into what content to consider for the long version and the short version - including how the ‘short name’ will be used  
- Moved the hint text up to just below the ‘question’ inputs, as suggested by one of the participants - as it felt dicsonnected from the content, and was displayed in a different order than the person filling in the form would see it  
  > P2: “This is a guidance note to that question, so I’d expect it to be directly underneath.”    
- Improved the hint text details link, and added more complete hint text for the hint text input. This is to give a better idea of what information might be useful to include here  
- Made the ‘answer’ types a question, “What kind of answer do you need to this question?” - using the previous hint text as the question, so we could inform users that the ‘answer’ types will validate based on the selected formats  
- Updated ‘answer’ radio options content to remove repetative content, “A(n)”, to reduce cognitive load and unnecessary repetition for screen reader users  
  - We also reordered this list to be alphabetical, while keeping what we thought would be the most common ‘answer’ type - “Single line of text” - at the top  
- “go to page list” updated to “Go to form overview” and moved to underneath the buttons to improve expectation management, and accessibility for users of zoom text technology  
- Content across the screen - and throughout the platform - that referred to ‘page’ changed to ‘question’ as that is more aligned with what the user is adding, editing, moving or deleting  

### Preview pane updates  
- Made the position absolute, so it no longer followed the user as they scrolled - this felt confusing and could cause accessibility issues
- Added a secondary heading to the right side, “Question preview” to help users understand what they should expect to see
- Removed the “Update preview” button from the right side, and made the primary call to action a “Save changes” button which will reload the page - with the newly updated preview
- Updated the preview link content to be more explicit about what the link will do “Preview question in a new tab”
- Disabled the button inside the preview pane, as this could cause accessibility issues or confuse users into thinking it was functional


![Newer version of edit question 1 page. Screenshot](../screenshots/005-Edit-question-1-hint-open.png)
*Page with “Question 1” caption above a heading “Edit question”.*

A secondary heading, “Question text”, comes directly before the hint text “Ask a question the way you would in person. For example ‘What is your address?’” and then a text input.

A second secondary heading, “Question short name (optional)”, followed by hint text “The short name will be used when the form’s questions are all displayed in a list. Use a short descriptive name. For example ‘Address’.” and then a text input.

Below these is a detail component, blue link with an arrow before the text, “Add hint text to help people answer the question” that is expanded. This reveals the hint text “You can use hint text if you need to explain the format the answer should be in, or where to find the information you’ve asked for.” before a text input.  

Next is a secondary heading, “What kind of answer do you need to this question?”, which has the hint text “The answer will be validated to check it’s in the selected format.” Below are radio buttons that determine the input type required:

- Single line of text, selected
- Address
- Date
- Email address
- National Insurance number
- Phone number

The page ends with a green “Save changes” button, next to a grey “Create next question” button before a red “Delete page” button. Below the three buttons is a “Go to form overview” link.  

<!-- describe side preview pane -->
On the right side of the screen there is a secondary heading, “Question preview” with a link to “Preview question in a new tab”.  

Below the link is a smaller version of an empty GOV.UK service page within an iframe, to mimic a mobile screen. It shows the GOV.UK logo on a black header. Within the body of the page is a disabled green ‘Continue’ button.  

### Feedback from testing this version 

- All users found the new hint text for ‘long’ and ‘short’ version of the question useful. It helped them understand what the difference is and how they might want to write their longer questions  
  > P1: “‘Ask a question the way you would in person’ - I like that wording. That’s clear.”  
  > P3: “This seems a lot clearer than the last time”  
- However, all users stated that they wouldn’t use ‘short’ version, as it’s still not entirely clear what the value of it is  
  > P1: “...the idea of this is good. I mean, my immediate thought is that it’s optional, why bother? What’s going to happen if I don’t opt to do that?”  
  > P2: “When they’re displayed in a list. What’s the list? Like a summary where they’re condensed?”  
- 2 users noticed the hint text, but didn’t comment on it having moved. 1 commented as though it wasn’t in the previous version  
  > P3: “I like that you now have an option to put something to explain the question”  
- Participant 1 made comment that the ‘delete question’ button was there when the page loaded, causing them confusion  
  > “Oh and you also have the option to delete a question - I think that’s new. It’s odd to have that here? You haven’t created a question so there’s nothing to delete. That’s confusing to be honest.”  
- Participant 1 also saw the ‘save changes’ button as an unnecessary step and just wanted to be moved on, and didn’t seem to notice the ‘create next question’ button. However, when they did save the question they noticed that the preview pane had updated offering a preview of the current screen as it would appear to the form filler  
  > “Oh so that’s different. That’s annoying. I’ve saved changes but then I have to click on the next question.”  
  > “Ah ok. So the preview isn’t really a preview. It’s just a preview of what I’m doing now.”  
  > “I would have liked to see it building as I go along - now I’m like what’s happened to my first question.”  
- Participant 2 was unsure about what would happen if they pressed to ‘create next question’. They were worried this would lose their progress  
  > “If I press create next question will it save what I’ve done? Or do I need to click Save changes first?”  
  > “I’d hope if I click next question it would save what I’ve done. But because there’s a save button next to it I’m not sure.”  
- Particiapnt 3 commented that they would always press the new ‘save changes’ button, and felt reassured that the page reloaded. This was seen as positive and gave them confidence that the save was made  
  > “Personally I would always do a save changes before I go to the next question. The fact that it’s refreshed itself makes me happy that it’s a saved question”  
- 2 users seemed to notice the preview pane after saving their question, 1 finding this useful to double check formatting before moving on. 1 user needed to be prompted by the user researcher before noticing the preview pane. The users questioned it’s usefulness and expected it to show the form as they built it  
  > P1: “I would have liked to see it building as I go along - now I’m like what’s happened to my first question.”  
  > P2: ask if the preview pane will show all of the questions: “That would be great. Without me having to use this button. But at the same time it’s helpful if you just want to check the one you’re looking at at the moment.”  
