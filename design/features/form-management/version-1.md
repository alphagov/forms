# Move a form to a different group 

## Status  

Date created: *2025-08-08*    

In development  

___   

## Contents   

- [Move a form to a different group](#move-a-form-to-a-different-group)  
  - [Contents](#contents)  
  - [What](#what)  
  - [Key decisions](#key-decisions)  
  - [Designs](#designs)  
 
___   

## What  

We want to allow org admins to move a form from one group to another.  

We need to design how they could do this and make sure it’s feasible from an implementation POV.  


## Key decisions  

- In July 2025 the [kick-off session explored what was in scope based on what we heard from existing org admin users](https://app.mural.co/t/gaap0347/m/gaap0347/1750068288725/f59f4a60d90f6e9b3c88cb418005c61e9bb7b32e)

As part of a follow up workshop the team explored potential design options to meet this need. In this session there was a clear consensus of a new simple journey to allow only org admins to move a single form between groups. We discussed: 

### Where we think we could start the journey

- Action on the form task list / live / archive view
- Action in the form table row

### What is in scope for the journey?

- Move a single form to another group
- Email notifications
  - Inform group admins that an org admin can move their form
  - Inform group editors that an org admin can move their form
- Limit the groups a form can be moved to based on the state of the form
- Use select component where the list of groups is larger that 11
- Extra: Reuse autocomplete component where the list of groups is larger that 31
- Warning org admins about the impact of a move - loss of access to some users

### What notifications are needed, and for who? 

- Notify other org admins of a forms move
- Notify the group admin of a forms move
- Notify the group editors of a forms move

### What is OUT of scope for now? 

- Moving multiple forms to another group
- Being able to quickly and easily see all the forms in your organisation, and which group they belong to
- Being able to move user permissions with a form
- Audit trails and historical changes
- Platform banner notifications

After playing back the options designed by the designers the team agreed to take forward [option 1 from teh mural area](https://app.mural.co/t/gaap0347/m/gaap0347/1752756571497/0452eaf50e2e6eb60472053cbd68c55b4f6e16a9?wid=0-1753696042341). This means adding a new link to “Change group” for each form on the group view page for org admins only. This design was then progressed into a [final option for development](https://app.mural.co/t/gaap0347/m/gaap0347/1752756571497/0452eaf50e2e6eb60472053cbd68c55b4f6e16a9?wid=0-1753883482071).  

## Designs  

### Your groups  
<img alt='“Your groups” organisation landing screen. Screenshot' src="screenshots-v1/001-your-groups.png" width="500">

Page titled ‘Your groups’ which lists the different groups within an organisation. This view shows what an organisation admin user would see. 

Table captioned ‘Upgrade requests’ with 2 columns, ‘Group name’ and ‘Created by’. The ‘group name’ table item shows the name of the group as a link to view and edit it. The ‘created by’ table item shows the firstname and lastname of the user who created the group. 

Below is another table captioned ‘Active groups. The table format is the same but this table only shows groups that are in an ‘active’ state. 

This is followed by a third table captioned ‘Trial groups’. 

The page ends with a green ‘Create a group’ button and closed details component labelled “What is a ‘group’?”.  

### Active group   
<img alt='“A wonderful group name” titled screen showing an ‘active’ group’s forms. Screenshot' src="screenshots-v1/002-active-group.png" width="500">

Page titled ‘A wonderful group name’, which is an example of what a group might be named. There is a caption above the heading, ‘Active group’, telling the user what state the current group is in. 

Beneath the heading are 2 links to edit this group: 

- Change the name of this group
- Edit the members of this group

Next is a green ‘Create a form’ button using the start button formatting with the right pointing arrow. 

Finally is a table captioned “Forms in ‘A wonderful group name’”. The table consists of 4 columns:  

- Form name
- Created by
- Status

And a newly added ‘Actions’ column which will only show for organisation admins. This column shows a ‘Change group’ link for each form. This is where the new journey is started from. 

The table in this example shows 3 forms: 

- Apply for a juggling licence
- Form a name
- Form b name 

### Move form to a different group  
<img alt='“Move form to a different group” titled screen with options of groups to move the form to. Screenshot' src="screenshots-v1/003-move-form-to-a-different-group.png" width="500">

Page titled ‘Move form to a different group’. There is a caption above the heading, ‘Active group’, telling the user what state the current group is in. 

Next is a summary list component playing back the information relevant to the person making the change to give some confidence that they are changing the correct form and group. It shows: 

- Form name: Apply for a juggling licence
- Group name: A wonderful group name

Next is some guidance content to help users understand the limitations and what happens when they save their changes. 

> You can move draft forms into active or trial groups. Live forms can only be moved into active groups.
>
> We’ll tell the group admins and editors that this form has been moved and they may no longer have access to it.

There is now a question for the user to answer, ‘What group do you want to move it to?’. In this version of the screenshot it shows 3 options listed as radio buttons: 

- Group a name
- Group b name
- Group c name

The radio options component is used where the options available are 10 or fewer. 

Finally, there is a green ‘Save and continue’ button.  

#### If there are no groups for this form to be moved to  
<img alt='“You have no other groups” option. Screenshot' src="screenshots-v1/003-move-form-to-a-different-group-no-groups.png" width="300">

When the user lands on this page and there are no options that meet the minimum criteria where the chosen form can be moved to the question and options list is replaced with static content: 

> **You have no other groups**
>
> You need to create a new group to move this form into, or upgrade a trial group to move a live form.

For this version we will also not show the ‘Save and continue’ button as the only action here should be to go back to the previous group view page.  

#### If there are between 11 and 30 potential groups this form can be moved to  
<img alt='What group do you want to move it to question with a dropdown select component. Screenshot' src="screenshots-v1/003-move-form-to-a-different-group-11-to-30-groups.png" width="300">

When the user sees this page where they have between 11 and 30 group options to choose from we will show a select component, this was agreed as a fall back to time there are over 11 options available. While an autocomplete component should be shown as the primary choice. 

### If there are more than 30 potential groups this form can be moved to 
<img alt='What group do you want to move it to question with an autocomplete component. Screenshot' src="screenshots-v1/003-move-form-to-a-different-group-31+-groups.png" width="300">

Where there are more than 30 groups to move a form to the list should as much as possible be shown as an autocomplete, only showing as a select component where javascript is disabled. 

#### Error message if no selection is made  
<img alt='“There is a problem” error banner. Screenshot' src="screenshots-v1/003-move-form-to-a-different-group-error.png" width="300">
*The error message shows ‘Select the group you want to move this form to’ which is a link to the page’s question input.*

This error will only appear where a user tries to ‘Save and continue’ without making a choice. This is the same error as it would appear no matter which component is shown. 

### Active group - successfully moved form to a new group   
<img alt='Active group page showing a success message. Screenshot' src="screenshots-v1/004-active-group-success-form-moved.png" width="500">

When a form is successfully moved from one group to another the user is returned to the group view page titled ‘Your groups’. There is a green ‘Success’ banner that now appears at the top of this page playing back the details of the change made to provide confidence that what the user has tried to do has taken effect. The message in this example says: 

> ‘Apply for a juggling licence’ has been moved to ‘Group a name’

The table captioned “Forms in ‘A wonderful group name’” further down the page now only shows 2 forms, no longer showing the ‘Apply for a juggling licence’ row as this form has been moved to another group in the organisation. 


### Notification email - Group admins and editors version 
<img alt='“Your form has moved groups” email to group admins and editors. Screenshot' src="screenshots-v1/101-form-moved-groups-email-group-admin-editors.png" width="500">

This is an example of the emails that group admins and editors will receive when a form that was in one of their groups is moved elsewhere. The intention is to make sure all impacted users are notified of the change and who it was made by and when. This email has the subject line: 

> Your form has moved groups

And the body reads: 

> The form “[form name]” has been moved from a group you are part of, “[group Y name]”, to the group “[group Z name]”.
>
> [org admin name] moved the form at 11:58am on 31 March 2025.
>
> You may no longer have access to this form.
>
> You are receiving this email because you are a form editor or a group admin for this group. You cannot unsubscribe from these emails.

Finally is some content explaining that this email is a no-reply email, as per the rest of the emails sent by GOV\.UK Forms. It reads: 

> **You cannot reply to this email**
>
> If you need to contact the person who made this change, you’ll need to contact them directly.
>
> If you’re experiencing a technical issue with this form, contact the GOV.​UK Forms team with details of the issue and the form it relates to.

### Notification email - Org admins version 
<img alt='“A form has been moved” email to org admins. Screenshot' src="screenshots-v1/102-form-moved-groups-email-org-admins.png" width="500">

This is an example of the email that organisation admins will receive when a form in their organisation is moved. The intention is to make sure all organisation admins are notified of the change and who it was made by and when so there is accountability and traceability. This email has the subject line: 

> A form has been moved

And the body reads: 

> The form “[form name]” has been moved from the group “[group Y name]” to the group “[group Z name]”.
>
> [org admin name] moved the form at 11:58am on 31 March 2025.

Finally is some content explaining that this email is a no-reply email, as per the rest of the emails sent by GOV\.UK Forms. It reads: 

> **You cannot reply to this email**
>
> If you need to contact the person who made this change, you’ll need to contact them directly.
>
> If you’re experiencing a technical issue with this form, contact the GOV.​UK Forms team with details of the issue and the form it relates to.

___   

<br>  

[Back to the top](#move-a-form-to-a-different-group)  
