#   Editor journey

## Status

- Date created: *2024-05-03*
- Developed 

## Contents
- [As is](#as-is)
- [To be](#to-be)
- [Key decisions](#key-decisions)
- [Designs](#designs)

## As is 
- Currently anyone who uses Forms can create a from and make it online
- Departments don't have a way to check which forms are being made.
- At the moment Adoption team manually updates users name and organisation. 

## To-be
Editor journey enables editors to:
- Create and edit a form
- View other members of the group

## Key decisions
- We decided to make the MVP version of this journey so we enable departments have control over their forms and learn more from the users.

**Select an organisation**
- Created an extra html page and  made it necessary for all users to select their organization after they logged in the Forms service. This helps the adoption team see if their department has an MOU. This process is only done once when the users signs in for the first time.
- We are using autofill feature with the search functionality. 
- Dev & Design team decided not to validate email addresses against name and organisation for this mvp.
- Added a details component to explain users what to expect if their organisation is not listed on the organisation list. This was done to help reduce support tickets.
- We decided to ask for users to input their organisation first to avoid users who can't use Forms yet.

**Groups landing page**
- Created an page for users to see groups they are part of while allowing them to create their own groups. We decided that whoever creates a group becomes a group admin and can only publish forms if they have their form upgraded by an organisation admin.

**Groups landing page with an upgrade request**
- Added an extra line for upgrade request so the users can see which groups have requested to upgrade.

 **Create a new group**
- Added a HTML page for users to create their group.

 **Group page with a form** 
- Added a HTML page to display forms in a group.
- Added a link to view members of the group

**View or edit members of this group**
- Added a HTML page to show a list of users.

 **Task list page-trial group**
- Using the same task list page and only changing the content for Make your form live.

 **Task list page-active group**
- Using the same task list page and only changing the back link to "back to <name of group> " and content for "Make your form live"

  
## Designs
- [Figma files for designs can be found here](https://www.figma.com/file/D2DtaS68qRvVZgtxaBQNjd/User-management---moving-to-a-'group'-model-for-public-beta?type=design&node-id=124%3A7025&mode=design&t=oXGvFNLZw5ETbTzV-1")
- [Protoype can be found here](https://forms-prototypes-pr-201.herokuapp.com/product-pages)
<br>

### Select an organisation 
![Select an organisation](/design/features/user-management/screenshots-v1/group-admin-screenshots/001-selectorganisation.png)
*This shows the ‘Select an organisation’ page with the new guidance section that says "Currently, GOV.UK Forms is only available for central government organisations that publish content on the GOV.UK website." It then asks user to select the organisation they work in, this is followed by a green, primary “Save and continue” button. Underneath the primary button there's a details component with a title "if your organisation is not listed" and a body text "If you’re from a central government organisation that publishes content on the GOV.UK website but your organisation is not listed, please contact the GOV.UK Forms team.If you’re from a public sector organisation that does not publish content on GOV.UK you cannot use GOV.UK Forms yet. You can read about our forthcoming features and sign up to our mailing list for updates.*

Once users select the organisation they are in, they are taken to Enter your full name page. 

If users don't select an organisation, we prevent them from moving forward and show the following error messaging: "There's a problem, select your organisation"

### Enter your full name
![Enter your full name](/design/features/user-management/screenshots-v1/group-admin-screenshots/002-enteryourfullname.png)
*This shows the ‘Enter your full name’ page and asks user to input their name and surname. It's then followed by green, primary button that says "Save and Continue"* 

Once user clicks "Save and continue" they are taken to groups landing page. 

### Groups landing page
![Your group](/design/features/user-management/screenshots-v1/group-admin-screenshots/003-yourgroup.png)
An example of a your group page. It shows:
- Active groups
- Trial groups
- Create a group primary button
- What is a 'group' detailed component with a text that says:

*Each form is created inside a group. People can be added to a group to create and edit forms in it. If you need access to an existing form or group, ask someone who has access to that group to add you. When a group is first created it will be a ‘trial’ group. That means you cannot make any forms in the group live. You can request for a group to be upgraded to an ‘active’ group if you need to make forms live. If you’re not sure if you should make a new group, speak with your organisation’s GOV.UK publishing team.*

Once 'create a group' is selected, a user is taken to create a new group page. 

### Create a new group
![Create a new group](/design/features/user-management/screenshots-v1/group-admin-screenshots/004-createanewgroup.png)
*This shows the ‘Create a new group’ page. It asks users to enter a name for their group. It is then followed by primary button that says 'Save and continue'.*

Once a user clicks the button they are taken to group page. 

### Group page
![Group landing page](/design/features/user-management/screenshots-v1/editor-screenshots/006-grouppageforatrialgroup.png)
This shows the group landing page where a user can see all the forms inside this group. With a functionality of viewing members of this group. 

### Members of this group
![Members of this page](/design/features/user-management/screenshots-v1/editor-screenshots/005-membersofthisgroup.png)
This shows the a list of members in a group.

### Task list page - trial
![Task list page](/design/features/user-management/screenshots-v1/editor-screenshots/007-tasklistpage-trial.png)
*Example of a task list page for a trial group with a changed content for Make your form live section. Changed content is as follows "This form cannot be made live because it’s in a ‘trial’ group. A group admin can request to upgrade the group so forms can be made live. You can view the members of the group to find a group admin.*

### Task list page - active
![Task list page](/design/features/user-management/screenshots-v1/editor-screenshots/007-tasklistpage-livegroup.png)
*Example of a task list page for an active group with a changed content for "Make your form live section". Changed content is as follows Only a group admin can make a form live. View the members of the group to find a group admin.*
