# Add guidance v1

## Status

Date created: *2023-10-03*  

Developed  

___

## Contents

- [Status](#status)
- [Contents](#contents)
- [What](#what)
- [Key decisions](#key-decisions)
- [Design for build](#design-for-build)
- [Design to test in the prototype](#design-to-test-in-the-prototype)
- [Notes](#notes)
- [Research focus](#research-focus)

___

<br>

## What

### As-is

- Form creators need to consider whether adding additional content to the hint text would make it too long and - if so - whether it would be better to have a longer question or add additional content to the start page

### To-be

- Form creators can add additional content and context to individual question pages to help form completers understand what's needed from them. They can use basic formatting like headings, lists and links.


## Key decisions

It was agreed that we'll build a minimum version that covers the basic functionality needed for this feature, while making it available as soon as possible so that more forms can be onboarded. 

In parallel, we'll design and test another version in the prototype. This version is a larger change to the overall flow of adding and editing a question, so we believe we need to validate it before commiting to development.

### What we will support
- Headings - second (H2) and third (H3) level only
- Paragraphs - allowing blocks of content that are clearly distinct from each other
- Lists - both bulleted and numbered lists
- Links:
  - support for simple URLs to guidance pages
  - these will not be validated as real URLs
  - clicked links will always open in a new window or tab
- Maximum of 5,000 characters - this does not include the Markdown tags
- Previewing Markdown as it will be displayed to the form completer: 
  - preview will be in page and will not include the question or input
  - preview will be enhanced using Javascript so users can quickly switch in page without a reload
- Basic WYSIWYG functionality for the Markdown textarea:
  - this will cover only the formatting we'll support, such as H2, H3, link, bulleted list and numbered list
  - this is a Javascript enhancement only
- Formatting help - guidance to help form creators write Markdown for supported formats, especially helpful where Javascript is disabled

### What we will not support
- Headings:
  - level 1 (H1) as this is covered by a separate input to ensure valid and accessible page markup
  - levels 4 to 6 (H4, H5, H6) as we believe this is unnecessary at this time, and adds more potential for missuse
- Bold - we believe that adding this now could cause missuse and potentially add more difficulty for form completers, but we'll keep an eye on it for future iterations
- Underline - we believe that this is not going to be needed for any of the forms on our platform, but we'll keep an eye on it for future iterations
- Tables - this is complex Markdown and we do not currently have a need to include it
- Blockquotes - this is something we don’t believe there will be a need for
- Inset text - this would be a custom piece of Markdown and there's currently no need to include it
- Notifications - this would be a custom piece of Markdown and there's currently no need to include it
- Warning text - this would be a custom piece of Markdown and there's currently no need to include it
- Code snippets - this is unlikely to be something we'll need to consider
- HR - this is unlikely to be something we'll need to consider

### Markdown errors
- We'll have an empty input error
- We'll have a character count error, triggering where character count is over 5,000 not including Markdown
- We believe we can offer some initial errors to cover unsupported formats
- We want to include validations on:
  - links:
    - has a URL been provided?
    - is it a valid URL?
    - is it an email address - is it valid?

<br>

## Design for build

### Edit question page

![Edit question page with new “Guidance” section and grey “Add guidance” button. Screenshot](https://github.com/alphagov/forms/assets/35372982/02f5af4e-9e46-4581-8d1b-992f8851d5b0)
*This shows the “Edit question” page with the new “Guidance” section, and the following explanatory text: “Only add guidance if you need to give a longer explanation of how to answer the question, or to format your content. For example, you can use paragraphs, links or lists.” This is followed by a grey, secondary “Add guidance” button.*  

The form creator can now add guidance if they need to give the form completer a longer explanation of how to answer the question. It also highlights that form creators can use this feature if they need to add formatting or links to their 'help' text.  

Once clicked, the form creator is then taken to the “Add guidance” page, which is a sub journey of the overall add/edit-a-question flow. This means they're taken out of the larger linear flow and will be returned after they've added whatever guidance content is needed.  

### Add guidance page - no Javascript

![Add guidance page with “Formatting help” expanded showing all of the guidance about formats and how to add or use them. Screenshot](https://github.com/alphagov/forms/assets/35372982/9eb8bf93-8d0b-4d52-9ecb-7e91f12268a6)

We explain when to use the guidance feature:
> Use guidance if you need to:
> - explain how to answer the question in more detail
> - provide more context
> - format your content - for example, with links, sub-headings or lists  

We then ask the user to “Give your page a heading”  
> Use a heading that’s a statement rather than a question - for example, ‘Interview needs’. This will be your main page heading.  

This is to make sure we have a clear H1 for the page.  

Next, they can add guidance text in a textarea using Markdown:  
> Use Markdown if you need to format your guidance content. Formatting help can be found below.  

They can then choose to “Update preview” to preview how the content will look to the form completer (on the frontend).
The button will reload the page and take the browser focus to the “Preview your guidance text” `<div>` to reduce confusion and scroll fatigue.  

Due to Javascript being disabled, the “Formatting help” details component will be expanded on page load. This does add more scolling and noise to the screen but it should at least be obvious and helpful to users - as they won’t have the WYSIWYG buttons. We're starting with content based on what Notify use, as they've done a lot of testing with a similar user type to us and have found that their implementation is working as expected. We'll monitor this through research.  

When a user has added their guidance and previewed it they may need to return to their guidance text to make quick changes or minor fixes. To avoid scrolling and reduce confusion we've added a link under the preview area to “Edit guidance text” - this moves focus back to the "Add guidance text" textarea further up the page.  

### Add guidance page - Javascript enhancement

#### Add guidance text

![Add guidance page showing the “Write” tab for form creators to write and edit their Markdown. Screenshot](https://github.com/alphagov/forms/assets/35372982/c12db057-f6e0-40e5-8e8d-1abaae0543ce)

Using the tab component from the design system we're reducing the scroll on this screen when Javascript is enabled. And we're able to help form creators quickly preview without the page reloading. We're also able to offer a limited WYSIWYG for adding or editing Markdown.  

#### Preview guidance text

![Add guidance page showing the preview of the guidance text as it would appear to the form completer. Screenshot](https://github.com/alphagov/forms/assets/35372982/4b8080c4-dfbf-4841-867b-af52802119c7)

#### Notes on Javascript-enhanced guidance text

We will need to test and validate whether:  
1. the use of the tab component works for our users and is accessible  
2. giving the supported formats as a WYSIWYG above the text area is helpful to our users, and verify that the implementation is accessible  
3. we can do error validation between the “Write” and “Preview” tabs using Javascript - making sure this is handled in an accessible way  

### Your questions - live form questions summary

![Your questions - live form summary cards for each question with the new guidance page heading and text included in a question page. Screenshot](https://github.com/alphagov/forms/assets/35372982/0a27ecce-7160-40e2-8718-f56a3263f30e)
*This screen shows the list of questions for a form that is ‘Live’ on GOV.UK Forms. It shows summary cards for each question in the form. The second question now has a row for “Page heading” and another for “Guidance text” as the form creator has added this. These rows appear as the first two rows in the card, above “Hint text” and “Answer type”.*  

### Add guidance error messages

![There is a problem - error summary components with messages that could appear at the top of the "Add guidance" page. Screenshot](https://github.com/alphagov/forms/assets/35372982/820bbfcb-856f-4698-9275-bec07d036baf)

Three errors as they could appear on the “Add guidance” page are:  
1. ‘Enter a page heading’ - where the form creator has not added a page heading  
2. ‘Enter guidance text’ - where the form creator has not added any guidance text  
3. ‘Guidance text can only contain formatting for links, subheadings (##), bulleted lists (*), or numbered lists (1.)’ - where the form creator has added invalid Markdown, such as a single hashtag (#) for a heading level 1 (H1)  

### Returning to the "Edit question" page

Once a user has added the guidance information required they are then returned to the “Edit question” page. Here, the guidance section has now turned into a summary list view where they can see the page heading and guidance text they've added - showing the Markdown. They have the option to “Change” either of these from here.  

#### "Edit question" return example for “Selection from a list” answer type

When a user returns to the “Edit question” page after adding their guidance information, if the answer type is “Selection from a list” they are not shown the “Question settings” section where they can make this question optional.  

![Edit question page with the “Guidance” section showing a summary list view of the information a form creator has added and the option to change their inputs. Screenshot](https://github.com/alphagov/forms/assets/35372982/508dfdee-a90e-4c25-a684-0fcb904f7937)

#### "Edit question" return example for most other answer types

When a user returns to the “Edit question” page after adding their guidance information, if the answer type is not a “Selection from a list” then they are still shown the “Question settings” section where they can make this question optional.  

![Edit question page with the “Guidance” section showing a summary list view. Next is the “Question settings” section allowing the form creator to make this question optional. Screenshot](https://github.com/alphagov/forms/assets/35372982/8dd85593-a13a-4032-a439-6fae5cf6065b)

<br>

#### Flow for intitial build

```mermaid
    
flowchart LR;

    step1["Edit your question
    [Add guidance]button
    "]
    
    step2["Add guidance
    Give your page a heading
    [input]
    Add guidance text
    [textarea]
    "]

    step1-->|"user clicks #quot;Add guidance#quot; button"|step2;
    step2-->|"user clicks #quot;Continue#quot; button"|step1;
    
```

<br>

## Design to test in the prototype

In order to explore an alternative option we agreed to test a more complex journey change in the prototype. This version removes the answer type summary list from the “Edit question” screen, no longer showing previous options selected to setup the question. It uses routing to build a complex question with additional guiidance.  

In the prototype we also wanted to test the introduction of a “Check your question” - summary - page at the end of creating a question. We wanted to know if adding another screen would be useful to form creators or make the journey more laborious.  

### “Edit question” page - without summary information

![“Edit question” page without “Answer settings” section. Screenshot](https://github.com/alphagov/forms/assets/35372982/93b852c7-d979-48fd-867a-db1381cb90a1)
*The “Answer settings” section has been replaced with “Do you need to add guidance to help people answer the question?”*

The new question uses similar help text as the build version: “Only add guidance if you need to give a longer explanation of how to answer the question, or to format your content. For example, you can use paragraphs, links or lists.”  

It can be answered ‘Yes’ or ‘No’. If answered ‘Yes’ the user is taken to add the additional guidance.  

### “Add guidance” page - no Javascript enhancement

![“Add guidance” page with textarea to “Add guidance text”. The page includes “Formatting help” that is always visible. Screenshot](https://github.com/alphagov/forms/assets/35372982/013a4230-fcf9-4781-bde2-a86188ac23d3)

We include the same guidance to explain when to use the guidance feature as the initial build version:  
> Use guidance if you need to:  
> - explain how to answer the question in more detail  
> - provide more context  
> - format your content - for example, with links, sub-headings or lists  

We do not ask for the ‘page heading’ at this point. We believe that this will help the user focus on the single task of adding their ‘help’ text. We ask for the ‘page heading’ at the end of the journey as they will have context of the question page as a whole.  

The form creator is now asked to “Add guidance text” with hint text: “Use Markdown if you need to format your guidance content. Formatting help can be found below.” Above a textarea with a character count below showing “You have 4000 characters remaining”. There is a grey “Preview guidance” button that updates the page and generates a preview of what the content will look like to form completers. The focus is moved to the ‘preview area’ to reduce scrolling. However, if the user is not re-focussed correctly they are presented with a green ‘success’ notifcation banner at the top of the page which links them to the ‘preview area’ when clicked.  

The next section is “Formatting help” which lists the supported Markdown the form creator can use when creating their guidance. We’re starting with content based on what Notify use, as they’ve done a lot of testing with a similar user type to us and have found that their implementation is working as expected. We'll monitor this through research. The form creator can either ‘continue’ using a green call to action button, or ‘cancel’ the addition of guidance - returning them to the “Edit question” page.  

#### “Add guidance” page with “Preview your guidance text” showing

The form creator is only presented with this view if they click “Preview guidance”. By clicking the green “Continue” button they will be moved on in the flow without first being presented with the ‘preview area’.  

![“Add guidance” page now also showing a green ‘success’ notification banner at the top. There is also a new “Preview your guidance text” section at the bottom of screen. Screenshot](https://github.com/alphagov/forms/assets/35372982/4771d1ae-dea4-4f8c-889b-079119c84c13)
*This is a version of the page where the user has added their ‘guidance text’ and clicked the “Preview guidance” button.*  

The new “Preview your guidance text” section gives a simple explanation of what the form creator is seeing in the ‘preview area’ box: “Below is a preview of how your guidance content will be shown to the person completing the question.”  

The ‘preview area’ shows the Markdown has been converted to a presentation of the HTML as interpreted by the browser. This means they are able to get an idea of how this will appear for form completers going through the form. Below the ‘preview area’ is a link - “Edit guidance text” - that the form creator can use to quickly take them back up the page to make edits or fixes to the Markdown they have written.  

If the user was to click the “Continue” call to action button they would move on to the “Check your question” summary page allowing them to review everything about this question.  


### “Check your question” page

#### No guidance text added  

![“Check your question” page summarising the information the form creator has provided to create their question. Screenshot](https://github.com/alphagov/forms/assets/35372982/e687f2aa-6f01-4ef9-8081-878008b62e65)

This page plays back the selections form creators have made to build their question.  
It starts with a section “Your question”. This section has a summary list with a row for each piece of information given. 
“Question”, “Hint text (optional” and “Add guidance” - which is set to “No” in this instance.  

The next section is “Answer settings” showing the “Answer type” - currently set as “Selection from a list of options”, so includes a row for “Options”, “People can only select one option” and “Include an option for ‘None of the above’”. Where a different “Answer type” is selected the user will have the additional answer information associated with that type here.  

#### Guidance text has been added  

![“Check your question” page showing “Give your page a heading” input. Screenshot](https://github.com/alphagov/forms/assets/35372982/7ce4e0a8-4273-4b85-8a1b-23e525827eca)

This page is now showing that the form creator has set “Add guidance” as “Yes”. There is a new row added to the “Your question” section called “Guidance text”. This row plays back the Markdown - as it was written. Where the content is consider to very long - length to be confirmed - we will hide overflow and add a “Show” link to expand the rest of the Markdown on click.  

The “Answer type” of this question is “Person’s name” so the second section “Question settings” can be seen. This section only contains a single row for “Make this questional optional” - currently set as “No” by the form creator.  

The next section “Answer settings” plays back the additional answer information associated with a “Person’s name” “answer type”.   

Because the form creator has chosen to ‘add guidance’ for this question. We present them with a new input. 
“Give your page a heading” which has some simple hint text - “Use a heading that’s a statement rather than a question - for example, ‘Interview needs’. This will be your main page heading.” The hint text is intended to help from creators create a useful heading for the page - making sure that the form is marked up correctly for accesibility, while remaining relevant to the information the form completer will see on screen. It also explains where this text will appear - giving the form creator more context of why we are asking for it.  


<br>

#### Flow of prototype tested

```mermaid
    
flowchart LR;

    step1["Edit your question
    Do you need to add more detail to help users answer the question?
    [] Yes
    [] No
    "]
    
    step2["Add guidance
    Add guidance text
    [textarea]
    "]
    
    step3["Check your question
    Summary list
    ---
    Give your page a heading
    [input]
    "]

    step1-->|"user answers #quot;Yes#quot; to add more detail"|step2;
    step2-->|"user clicks #quot;Continue#quot; button"|step3;
    
```

<br>

## Notes

- As part of the first iteration we are attempting to create a new custom graphical interface that helps users add/edit Markdown by use of buttons
  - This functionality will need usability and accessibility testing
  - We won’t be testing this component as part of this iteration and should focus on it in a future round of research before we consider re-using it on other screens within the product
- The implementation we are taking into development is at risk as we are currently unsure if the ‘formatting help’ and other parts of the guidance are going to help our users
  - We believe this is a low risk and that by putting this in the product we will get better quality feedback and a better understanding of how our users are using the feature

___

<br>

## Research focus

### Things we plan to focus on in testing:
- Testing the new journey for adding questions
- Testing user experience for adding detailed guidance
  - Do they understand what the feature is?
  - Are they able to distinguish detailed guidance from hint text?
  - Are they likely to use the correct feature for their need?
  - Do users understanding why they are being asked for a ‘page heading’?
- Testing user experience for formatting with markdown
  - Can users write/create working Markdown based on a document version of a form?
  - Do users find the ‘formatting help’ useful, and are they able to fix issues themselves?
-  Although not priority, we will keep an eye on how users interact with and what they say about the “Check your question” summary page
  - Do users like it?
  - Do users find it useful?
  - Do users feel like it adds another barrier to creating questions, or does it give them confidence that the question they are creating will be correct?
  - Is there anything they were or were not expecting about the journey/page in particular?  

[Research plan/discussion guide](https://docs.google.com/document/d/14Omvdh5-ck9A8NoPzB7TbF5mTpzVRoHU0oCODcJzAPg/edit#heading=h.d7qnjjmaxy08)  

### Update: what we found through testing  

[Playback: User Research - Detailed Guidance (Google slides)](https://docs.google.com/presentation/d/1cZKLrPDaXZlqHtg_y8rYE2eKA1B26Hc8YiUBJKGc-jg/edit#slide=id.g2793e27bf4a_0_65)  
[UR Playback: Detailed Guidance (Video)](https://drive.google.com/drive/folders/1L52JCUb8hLea32lS5im6mM7Y4AKhZGWV)  

<br>

___

<br>

[Back to the top](#add-guidance-v1)
