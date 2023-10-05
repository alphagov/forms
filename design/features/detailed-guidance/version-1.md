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

- Form creators need to consider if adding additional content to the hint text is too much, or if it makes more sense to have a longer question or additional content on the start page

### To-be

- Form creators can add additional content and context to individual question pages, using some basic formatting including headings, lists and links to support form completers at their time of need


## Key decisions

It was agreed that we will build a minimum version that covers the basic functionality making sure we are able to offer the feature to allow more forms to be onboarded. In parallel we will design and test another version in the prototype. This version is a larger change to the overall flow of adding and editing a question and so we believe we need to validate before commiting to development.

### We agreed that we will support
- Headings - second (H2) and third (H3) level only
- Paragraphs - allowing blocks of content that are clearly distinct from each other
- Lists - both bulleted and numbered lists
- Links
  - support for simple URLs to guidance pages
  - these will not be validated as real URLs
  - clicked links will always open in a new window or tab
- Maximum of 5000 characters - this does not include the markdown tags
- Previewing markdown as it will be displayed to the form completer 
  - preview will be in page and not include the question or input
  - preview will be enhaced using javascript so users can quickly switch in page without a reload
- Basic WYSIWYG functionality for the markdown textarea
  - this will only cover the formatting we will support such as, H2, H3, link, bulleted list and numbered list
  - this is a javascript enhancement only
- Formatting help - guidance to help form creators write markdown for supported formats, especially helpful where javascript is disabled

### We will not support
- Headings
  - level one (H1) as this is covered by a separate input to ensure valid and accessible page markup
  - levels four to six (H4, H5, H6) as we believe this to be unnecessary at this time, and adds more potential for missuse
- Bold - we believe that adding this now could cause missuse and potentially add more difficulty for form completers, but will keep an eye on for future iterations
- Underline - we believe that this is not going to be needed for any of the forms on our platform, but will keep an eye on for future iterations
- Tables - this is complex markdown and we curently do not have a need to include this
- Blockquotes - this is something that we don’t believe there will be a need for
- Inset text - this would be a custom piece of markdown and currently there is no need to include it
- Notifications - this would be a custom piece of markdown and currently there is no need to include it
- Warning text - this would be a custom piece of markdown and currently there is no need to include it
- Code snippets - this is unlikely to be something we will need to consider
- HR - this is unlikely to be something we will need to consider

### Markdown errors
- We will have an empty input error
- We will have a character count error, triggering where character count is over 5000 not including markdown
- We believe we can offer some initial errors to cover unsupported formats
- We want to include validations on
  - links
    - has a URL been provided
    - is it a valid URL
    - is it an email address - is it valid

<br>


## Design for build

### Edit question page

![Edit question page with new “Guidance” section and grey “Add guidance” button. Screenshot](https://github.com/alphagov/forms/assets/35372982/02f5af4e-9e46-4581-8d1b-992f8851d5b0)
*This shows the “Edit question” page with the new “Guidance” section, and the explanation text: “Only add guidance if you need to give a longer explanation of how to answer the question, or to format your content. For example, you can use paragraphs, links or lists.”. Followed by a grey secondary “Add guidance” button.*

The form creator can now add guidance, if they need to give a longer explanation of how to answer the question to the form completer. It also highlights that they can use this feature if they need or want to add formatting or links to their help text.  

Once clicked the form creator is then taken to the “Add guidance” page which is a sub journey of the overall add/edit a question flow, meaning they are taken out of the larger linear flow to be returned after they have added the guidance content they need.


### Add guidance page - no javascript

![Add guidance page with “Formatting help” expanded showing all of the guidance about formats and how to add or use them. Screenshot](https://github.com/alphagov/forms/assets/35372982/9eb8bf93-8d0b-4d52-9ecb-7e91f12268a6)

We explain when to use the guidance feature:
> Use guidance if you need to:
> 
> - explain how to answer the question in more detail
> - provide more context
> - format your content - for example, with links, sub-headings or lists

We then ask the user to “Give your page a heading”
> Use a heading that’s a statement rather than a question - for example, ‘Interview needs’. This will be your main page heading.

This is to make sure we have a clear H1 for the page.

Next they can add guidnce text in a testarea using markdown:
> Use Markdown if you need to format your guidance content. Formatting help can be found below.

Before they can “Update preview” to see what the content will look like as it would appear to the form completer (on the frontend).
The button will reload the page and take the browser focus to the “Preview your guidance text” `<div>` to reduce confusion and scroll fatigue.  

Due to javascript being disabled the “Formatting help” details component will be expanded on page load, which does add more scolling and noise to the screen but should be obvious and helpful to users - as they won’t have the WYSIWYG buttons. We are starting with the content used in Notify as they have done a lot of testing with a similar user type to us and have found that their implementation is working as expected. We will monitor this through research.  

When the user has added their guidance and previewed it they may need to return to make quick changes or minor fixes. To avoid scrolling and reduce confusion we have added a link under the preview area to “Edit guidance text” which moves focus back to the add guidance text textarea further up the page.  


### Add guidance page - javascript enhancement

#### Add guidance text
![Add guidance page showing the “Write” tab for form creators to write and edit their markdown. Screenshot](https://github.com/alphagov/forms/assets/35372982/c12db057-f6e0-40e5-8e8d-1abaae0543ce)

Using the tab component from the design system we are reducing the scroll on this screen when javascript is enabled. And are able to help form creators quickly preview without the page reloading. We are also able to offer a limited WYSIWYG for adding or editing markdown.  

#### Preview guidance text
![Add guidance page showing the preview of the guidance text as it would appear to the form completer. Screenshot](https://github.com/alphagov/forms/assets/35372982/4b8080c4-dfbf-4841-867b-af52802119c7)

#### Notes on javascript enhanced guidance text

We will need to test a validate if:
1. the use of the tab component works for our users and is accessible
2. giving the supported formats as a WYSIWYG above the text area is helpful to our users and verify that the implementation is accessible
3. we can do error validation between the “Write” and “Preview” tabs using javascript - making sure this is handled in an accessible way


### Your questions - live form questions summary

![Your questions - live form summary cards for each question with the new guidance page heading and text included in a question page. Screenshot](https://github.com/alphagov/forms/assets/35372982/0a27ecce-7160-40e2-8718-f56a3263f30e)
*This screen shows the list of questions of a form that is ‘Live’ on GOV.UK Forms. It shows summary cards for each question in the form. With the second question now having a row for “Page heading” and one for “Guidance text” as the form creator had added it. These rows appear as the first two rows in the card above “Hint text” and “Answer type”.*


### Add guidance error messages

![There is a problem - error summary components with messages that could appear at the top of the add guidance page. Screenshot](https://github.com/alphagov/forms/assets/35372982/820bbfcb-856f-4698-9275-bec07d036baf)

Three errors as they could appear on the “Add guidance” page are
1. ‘Enter a page heading’ - where the form creator has not added a page heading
2. ‘Enter guidance text’ - where the form creator has not added any guidance text
3. ‘Guidance text can only contain formatting for links, subheadings (##), bulleted lists (*), or numbered lists (1.)’ - where the form creator has added invalid markdown, such as a single hashtag (#) for a heading level 1 (H1)


### Returning to the edit question page

Once a user has added the guidance information required they are then returned to the “Edit quesiton” page where the guidance section has now turned into a summary list view where they can see the page heading and guidance text they added - showing the markdown. They have the option to “Change” either of these from here.

#### Edit question return example for “Selection from a list” answer type

When a user returns to the “Edit question” page after adding their guidance information, if the answer type is “Selection from a list” then they are not shown the “Question settings” section where they can make this question optional. 

![Edit question page with the “Guidance” section showing a summary list view of the information a form creator has added and the option to change their inputs. Screenshot](https://github.com/alphagov/forms/assets/35372982/508dfdee-a90e-4c25-a684-0fcb904f7937)

#### Edit question return example for most other answer types

When a user returns to the “Edit question” page after adding their guidance information, if the answer type is not a “Selection from a list” then they are still shown the “Question settings” section where they can make this question optional. 

![Edit question page with the “Guidance” section showing a summary list view. Next is the “Question settings” section allowing the form creator to make this question optional. Screenshot](https://github.com/alphagov/forms/assets/35372982/8dd85593-a13a-4032-a439-6fae5cf6065b)

<br>

#### flow

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

### page

![detail. Screenshot.](url)
*description*

<br>

#### flow

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

- 

___

<br>

## Research focus

### Scenarios to test (prioritised for time):
- 


<br>

___

<br>

[Back to the top](#add-guidance-v1)
