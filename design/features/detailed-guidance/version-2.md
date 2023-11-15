## Status
Date created: *2023-11-14*  

Developed: 

___

## Contents

- [Status](#status)
- [Contents](#contents)
- [What we’re doing](#what-were-doing)
- [Why we’re doing this](#why-were-doing-this)
- [Key decisions](#key-decisions)
- [Designs](#designs)

___

## What we’re doing
We’re making some content updates to the GOV.UK Forms ‘detailed guidance’ in response to findings from our first round of usability testing on this feature.

As a result of the findings, we’re going to:

* clarify the hint text and guidance instructions on the ‘Edit question’ page
* iterate the Markdown help text on the ‘Add guidance’ page
* clarify why a ‘page heading’ is needed when adding guidance

### Version 1 detailed guidance feature (as-is)

#### Hint text and guidance instructions - ‘Edit question’ page
The original hint text wording followed one of these patterns: 

* “Use hint text to help people answer the question” - along with an example relevant to the type of question (such as “For example, ‘You can provide either a home or mobile phone number.”) 
* ‘‘You could use hint text to tell people how you’ll use their address. For example, ‘We’ll send your licence to this address.’” 

The original guidance wording was: 

“Only add guidance if you need to give a longer explanation of how to answer the question, or to format your content. For example, you can use paragraphs, links or lists.”

#### Markdown help text - ‘Add guidance’ page

The original Markdown help text was as follows:  

“[H2] Formatting help

[H3] Links and URLs

To add a link, use square brackets [ ] around the link text, and round brackets ( ) around the full URL. For example:

> [Link text](https://www.gov.uk/link-text-url)

[H3] Second-level headings

To add a second-level heading, use 2 hashtags followed by a space. For example:

> This is a second-level heading

[H3] Third-level headings

For a third-level heading, use 3 hashtags followed by a space. For example:

> This is a third-level heading

[H3] Bulleted lists

To add bullet points, start each item with * (asterisk) or - (dash). Use one space after the asterisk or dash.

You need one empty line space before the bullets start, and one at the end. For example:

> * First bullet point
> * Second bullet point
> * Third bullet point

[H3] Numbered lists

Use numbers for each list item, followed by a full stop. Make sure there is one space after the full stop.

You need one empty line space before the numbers start, and one at the end. For example:

> * First item
> * Second item
> * Third item”

#### Clarify why a page heading is needed when adding guidance - ‘Add guidance’ page
The original content telling form creators they needed to add a page heading when using guidance, under the label “Give your page a heading”, was: 

“Use a heading that’s a statement rather than a question - for example, ‘Interview needs’. This will be your main page heading.”

### Version 2 detailed guidance feature (to-be)

#### Add brief clarification to hint text and guidance instructions - ‘Edit question’ page
In testing, the concept of detailed guidance came across relatively clearly. Some users started off creating long hints, but when they saw the option for guidance they sorted the information into a short hint and longer detailed guidance. However, we felt we could clarify the difference between hint text and detailed guidance. 

We considered various changes to hint text, like ‘no more than 1 or 2 sentences’, or ‘1 or 2 sentences only, no formatting’. In the end, however, we decided this could seem a bit suggestive or prescriptive and went with the simple addition of the word ‘short’ before the word ‘hint’. There’s a 500 character ‘hard’ limit in place, so if people go beyond that they’ll get an error message.

New ‘Hint text (optional)’ wording: “You can add a short hint to help people answer the question”. (This is followed by an example of possible hint text, which is customised to match the ‘answer type’.) 

For the guidance text, we decided to specify the exact formatting that will be allowed - rather than to say what it could ‘include’, which might lead people to think they could add more Markdown formatting than is possible.

New ‘Guidance’ wording: “Only add guidance if you need to give a longer explanation of how to answer the question, or to format your question with paragraphs, links, lists or headings.” 

See [Mural board for the updated content designs](https://app.mural.co/t/gaap0347/m/gaap0347/1683038152877/e16c675d20fcbc7595d016d03eeb5d7024fe0020?wid=0-1695202191757) 

#### Iterate Markdown help text - ‘Add guidance’ page
In testing, the experienced Markdown user found it very intuitive. They tried some advanced things not implemented but this didn’t cause an issue. 

Using the preview, along with some trial and error, most other users were able to set up at least some formatting, including hyperlinks.

However, correct use of spaces after bullets, and the fact that there should be no spaces in between elements of links caught some people out - particularly when a long link wraps over several lines in the input box.

The line spacing needed to correctly format a bulleted list did not come across clearly from the guidance to several users.

We decided to make the following changes to try and address these issues: 

* Under ‘Links and URLs’ added the sentence “Make sure there are no spaces between the two sets of brackets.” This is because some users left a space and struggled to understand why the link didn't work. This is very similar to the language used by GOV.UK and Notify.

* Added a new H3 ‘Headings’, followed by content explaining heading order in general, and the fact that headings shouldn't be used to achieve bold formatting, which is what one user did during testing. New content: “Use the headings in sequence - a second-level heading needs to come before a third-level heading. Do not use headings to style your text in bold. This can cause issues for people using assistive technology.”

* Made ‘Second-level headings’ and ‘Third-level headings’ H4s. Retained the examples from the first iteration but added the abbreviations ‘H2’ and ‘H3’ as these are in common usage and it makes sense to include them.

* Under H3 ‘Bulleted’ lists, changed “You need one empty line space before the bullets start, and one at the end” to “Leave one empty line before adding the first bullet point and another after the last bullet point.” This is because the GOV.UK terminology of leaving one 'empty line space' didn't test that well and some users seemed unclear about what was needed. Also changed the word ‘Use’ to “Make sure you use” in the sentence “Make sure you use one space after the asterisk or dash.” This was to emphasise the importance of this space. 

* Under H3 ‘Numbered lists’ made the same changes as for H3 ‘Bulleted lists’ (though already said “Make sure you use [...]”).

See Trello cards: 

* [Update Markdown help text](https://trello.com/c/6QDu4FMb/1009-guidance-update-markdown-help-text)
* [Add content to explain that headings shouldn’t be used for bold text](https://trello.com/c/9A1AFSW1/1016-guidance-add-content-to-explain-that-headings-shouldnt-be-used-for-bold-text)


#### Clarify why a page heading is needed when adding guidance - ‘Add guidance’ page
There was some confusion around why a page heading was needed during the first round of testing on this feature, even though users generally figured it out after a process of trial and error.

It’s worth noting that we tested this in the prototype version, which is different to what we have in Production. The prototype version was potentially more confusing as the ‘Give your page a heading’ section was at the bottom of the ‘Check your answers’ page and users therefore had less context. 

In Production, the ‘Give your page a heading’ section is part of the ‘Add guidance’ page itself, which maybe gives more context. However, we decided to update this content anyway, as the reason for needing a page heading is related to accessibility and isn’t at all obvious. 

New wording on the ‘Add guidance’ page:

“Use guidance if you need to:

* explain how to answer the question in more detail
* format your content with paragraphs, headings, lists or links
* Guidance will be displayed at the top of the page, above your question

[Label] Give your page a heading

When you add guidance your question text will no longer be the main page heading, so you need to use a different one. Use a heading that’s a statement rather than a question - for example, ‘Interview needs’.”

See Trello card ['Clarify why a page heading is needed for guidance'](https://trello.com/c/gVtM7i1U/1087-guidance-consider-clarifying-why-a-page-headings-needed-for-guidance) 

## Why we’re doing this
After an initial round of usability testing on detailed guidance, we decided to address changes that were considered important enough to prioritise.

We had to balance any improvements with the need to move onto the next GOV.UK Forms feature as quickly as possible in order to meet our roadmap commitments.

We decided to prioritise these particular tasks as they were seen as relatively ‘quick wins’ and would significantly improve form creators’ ability to use hint text and guidance effectively. 

## Key decisions
The main decision was to iterate some of the content to clarify:

* the difference between hint text and guidance
* how to use the Markdown formatting that’s available 
* why a new page heading is needed if you’re using guidance

## Designs

### ‘Edit question’ page - updated wording helps differentiate hint text and guidance

The explanatory text under the “Hint text (optional)” label now includes the word ‘short’: “You can add a short hint to help people answer the question.”

The explanatory text under the “Guidance” H2 clarifies what type of formatting is possible: “Only add guidance if you need to give a longer explanation of how to answer the question, or to format your content with paragraphs, headings, lists or links.”

![Updated hint text and guidance content. Screenshot](/design/features/detailed-guidance/screenshots-v2/hint-text-guidance-text-on-edit-question-page.png)


### ‘Add guidance’ page - updated text clarifies when to use guidance and how it will be displayed

There are now only 2 bullet points explaining that you should use guidance if you need to - “explain how to answer the question in more detail” or “format your content with paragraphs, headings, lists or links”.

A new sentence explains where guidance content will be shown: “Guidance will be displayed at the top of the page, above your question.”

[ADD SCREENSHOT 2]

### ‘Add guidance’ page - updated Markdown guidance clarifies how to use it correctly

The formatting help that’s revealed if someone clicks on the ‘Formatting help’ details component has been updated. It now clarifies how to use Markdown for links (no spaces between brackets) and lists (one line space is needed before and after the list items). 

It also has a new “Headings” H3, with information explaining that headings should not be used to achieve bold formatting.

[ADD SCREENSHOT 3]

### ‘Add guidance’ page - updated explanation of why a page heading is needed 
The explanatory content under the “Give your page a heading” label has been updated for clarity. 

It now says:  “When you add guidance your question text will no longer be the main page heading, so you need to use a different one. Use a heading that’s a statement rather than a question - for example, ‘Interview needs’.”

[ADD SCREENSHOT 4]

