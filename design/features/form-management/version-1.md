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

### Where we think we could start the journey?

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

Table captioned ‘Upgrade requests’ with 2 columns, ‘Group name’ and ‘Created by’. The group name table item shows the name of the group as a link to view and edit it. The created by table item shows the firstname and lastname of the user who created the group. 

Below is another table captioned ‘Active groups. The table format is the same but this table only shows groups that are in an ‘active’ state. 

This is followed by a third table captioned ‘Trial groups’. 

The page ends with a green ‘Create a group’ button and closed details component labelled “What is a ‘group’?”.  

### Active group   
<img alt='“A wonderful group name” titled screen showing an active groups forms. Screenshot' src="screenshots-v1/002-active-group.png" width="500">

Pge titled ‘A wonderful group name’, which is an example of what a group might be named. There is a caption above the heading, ‘Active group’, telling the user what state the current group is in. 

Beneatht the heading are 2 links to edit this group: 

- Change the name of this group
- Edit the members of this group

Next is a green ‘Create a form’ button using the start button formatting with the right pointing arrow. 

Finally is a table captioned “Forms in ‘A wonderful group name’”. The table consists of 4 columns:  

- Form name
- Created by
- Status

And a newly added ‘Actions’ column which will only show for organisation admins. This column shows a ‘Change group’ link for each form. This is where the new journey is started from. 

### Move form to a different group  
![“Move form to a different group” titled screen with options of groups to move the form to. Screenshot](./screenshots-v1/003-move-form-to-a-different-group.png)  

#### If there are no groups for this form to be moved to  
![You have no other groups option. Screenshot](./screenshots-v1/003-move-form-to-a-different-group-no-groups.png)  

#### If there are between 11 and 30 potential groups this form can be moved to  
![What group do you want to move it to question with dropdown select component. Screenshot](./screenshots-v1/003-move-form-to-a-different-group-11-to-30-groups.png)  

### If there are more than 30 potential groups this form can be moved to 
![What group do you want to move it to question with automcplete component. Screenshot](./screenshots-v1/003-move-form-to-a-different-group-31+-groups.png)  

#### Error message if no selection is made  
![There is a problem error banner. Screenshot](./screenshots-v1/003-move-form-to-a-different-group-error.png)  
*Error message shows ‘Select the group you want to move this form to’ which is a link to the pages question input.*


### Active group - successfully moved form to a new group   
![Active group page showing a success message. Screenshot](./screenshots-v1/004-active-group-success-form-moved.png)  


### Notification email - Group admins and editors version 
![Form has been moved email to group admins and editors. Screenshot](./screenshots-v1/101-form-moved-groups-email-group-admin-editors.png)  


### Notification email - Org admins version 
![Form has been moved email to org admins. Screenshot](./screenshots-v1/102-form-moved-groups-email-org-admins.png)  

___   

<br>  

[Back to the top](#move-a-form-to-a-different-group)  
