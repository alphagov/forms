# Organisation Admin Journey
## Status

- Date created: *2024-05-21*
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
Organisation admin journey enables organisation admins to: 
- View and remove members of a group
- Create and edit a form
- Add editors or group admins to a group 
- Make a form live and archive it (when group is ‘active’)
- Review upgrade requests and make groups active
- View all groups and forms in the organisation
- View all users in the organisation

## Key decisions
- We decided to make the MVP version of this journey so we enable departments have control over their forms and learn more from the users.

**Select an organisation**
- Created an extra html page and  made it necessary for all users to select their organization after they logged in the Forms service. This helps the adoption team see if their department has an MOU. This process is only done once when the users signs in for the first time.
- We are using autofill feature with the search functionality. 
- Dev & Design team decided not to validate email addresses against name and organisation for this mvp.
- Added a details component to explain users what to expect if their organisation is not listed on the org list. This was done to help reduce support tickets.
- We decided to ask for the organisation first to avoid users who can't use Forms yet. 

**Enter your full name**
- Created an extra a page and made it necessary for all users to fill in their name, so that we update our records about the user and the adoption team can check if an MOU is in palce.
  
**Groups landing page**
- Create an page for group admins to see all the groups in their organisation.

**Groups landing page with an upgrade request**
- Added a line to the upgrade request notification to ensure organization admins are aware of incoming requests

 **Create a new group**
- Added a HTML page for users to create their group.

 **Group landing page with a form** 
- Added a HTML page to display forms in a group.
- Added a link to change the name of this group
- Added a link to edit members of this group
- Added a notification banner to show a request to upgrade

 **View or edit members of this group**
- Added a HTML page to show a list of users.
- Added a green primary button to add an editor
- Added a gray secondary button to remove editors
- Added a gray secondary button to make a user group admin or an editor
- Added a details component to explain the difference between 'editor' and 'group admin' roles.

**Upgrade page - (with an upgrade request)**
- Added a HTML page to help organisatin admins upgrade a group
- Added a radio button with a 'yes' or 'no' option enabling organisation admins accepting or rejecting an upgrade request.
- Content we use in this page is different than Upgrade page - (without an upgrade request) page

**Upgrade page - (without an upgrade request)**
- Added a HTML page to help organisatin admins upgrade a group
- Added a radio button with a 'yes' or 'no' option enabling organisation admins accepting or rejecting an upgrade request.
- Content we use in this page is different than Upgrade page - (with an upgrade request) page
  
 **Group page for active group**
- Changing "trial" caption to "active".

 **Add another member**
- Added a HTML page for group admins to add other members to their group.
- Added a radio button enabling organisation admins assign a role (Editor or group admin) to a user.

 **Task list page-trial group**
- Using the same task list page and only changing the content for Make your form live.

 **Task list page-active group**
- Using the same task list page and only changing the back link to "back to <name of group> ".

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

Once user clicks "Save and continue" they are taken to your group page. 

### Groups landing page
![Your group](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/003-Grouplandingpage.png)

### Create a new group
![Create a new group](/design/features/user-management/screenshots-v1/group-admin-screenshots/004-createanewgroup.png)
*This shows the ‘Create a new group’ page. It asks users to enter a name for their group. It is then followed by primary button that says "Save and continue".*

Once a user clicks the button they are taken to Group landing page. 

### Group landing page with a form
![Group landing page](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/004-Grouplandingpage.png)

### Members of this group
![Members of this page](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/005-Membersofthisgroup.png)
This shows the a list of members in a group with a functionality of removing or adding members to this group. And a functionality to make a user an editor or group admin

Once a user clicks "add an editor or group admin". They are taken to add another member page. 

### Add another member to the group
![Add another member to the group](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/009-Addmembers.png)
This shows the ‘add another member to the group’ page and asks user to input email address of the user they want to add to a group as well as a role assigned to them. For example, group admin or editor roles. 

### Upgrade group  - With a request
![Upgrade this group](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/007-Upgradethisgroup.png)
This shows the ‘Upgrade group’ page and asks user to select 'yes' or 'no' radio buttons to upgrade a group.

### Upgrade a group - Without a request
![Upgrade this group](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/007-Upgradethisgroup2.png)
This shows the ‘Upgrade group’ page and asks user to select 'yes' or 'no' radio buttons to upgrade a group.

### Group landing page - Active 
![Upgrade this group](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/008-Activegroup.png)
An example of an active group. 

### Task list page- Active 
![Task list page](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/010-tasklistpage-active.png)
An example of a task list page in an active group.

### Task list page- Trial
![Task list page](/design/features/user-management/screenshots-v1/organisation-admin-screenshots/010-tasklistpage-trial.png)
An example of a task list page in a trial group. 
