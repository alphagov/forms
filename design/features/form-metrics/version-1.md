# Metrics for form creators v1

## Status

Date created: *2023-10-18*  

Developed  

___

## Contents

- [Status](#status)
- [Contents](#contents)
- [What](#what)
- [Key decisions](#key-decisions)
- [Design for build](#design-for-build)
- [Notes](#notes)
- [Research focus](#research-focus)

___

<br>

## What

### As-is

- Our performance analyst sends a manual report to form creators (OR main contacts)  

#### What have we been sending  

- In order of importance for service teams 
    1. Submissions
    2. Completion rate
    3. Question funnel
- Previously supplied: Questions amended from the check answers page - these are low in number, users seem more likely to use the browser forward/back buttons
- Submissions and completion rates over time
- Drop out/pain points
- Ability to download raw data
- Some of the Google Analytics metrics such as device type if/when we implement that on the forms runner (doing anything ourselves would be fraught with data privacy issues). They could then self serve these  

### To-be  

- Form creators can look at basic data relating to their forms performance  
- Admins from OGDs to be able to see the performance of all of their OGD forms  


## Key decisions

### What we will offer

- Number of submitted forms
- Number of unfinished forms - started but not complete
- Completion rate - as a percentage (%)
- A snapshot of the last week of data
  - This will only cover the previous 7 days
  - The previous 7 days will include the day previous to form creator looking but not todays data
  - It will change depending when the user looks at the form, day-to-day
 
### What we won’t offer

- No option to filter dates
- No data over 7 days old
  - Form creators can still ask us to manually produce this information, but is not to be expected
- No question funnel showing the drop outs at a page level
  - This is something we currently provide, and has been used to make improvements to forms when first going live
  - This is something we will try to look at in a future iteration, once we are confident in the data collection method

<br>

## Design for build

### Live form view with no metrics available as the form has just gone live

![Live form view with “No metrics available yet as no-one has started or submitted a form since it went live” message. Screenshot](https://github.com/alphagov/forms/assets/35372982/5ddfaa3a-3a02-43df-b58a-8c4cf39d6664)  

When form creators first make their forms live they and go to view their form. They will be presented with the ‘live’ state view of their form with the details they added to create their form.   

As part of this screen we will introduce a placeholder for the “Form metrics for the past 7 days”.   
Within this section form creators are presented with inset text telling them:  

> No metrics are available yet as no-one has started or submitted a form since it went live.  
> Once they have, you’ll be able to see the following for the past 7 days.  
>  
> - Completion rate  
> - Number of forms completed  
> - Number of forms started but not completed  

The rest of the screen has no changes, showing the rest of the form information including a way to preview their form.  

### Live form view with less than 7 days of metrics data

![Live form view with 3 days of metrics data. Screenshot](https://github.com/alphagov/forms/assets/35372982/8ea09690-ed56-4777-9c1c-2798659d54c3)  

This version of the ‘live’ form view now shows the form creator that they are seeing “Form metrics for the past 3 days: 29 September to 1 October 2023”.  

There is a paragraph at the start of this section telling the form creator what to expect is included in the data:  
> The metrics shown here are for less than a week. To see a full week's data, check again when your form's been live for 7 days.  

They are then present with 3 separate pieces of data displayed next to each other as though blocks.  

The first box shows “Completion rate” with the figure “87%” beneath it.  

The second box shows “Forms submitted” with the figure “87” beneath it.  

The third box shows “Forms started but not completed” with the figure “13” beneath it.  

### Live form view with 7 days of metrics data

![Live form view with 7 days of metrics data. Screenshot](https://github.com/alphagov/forms/assets/35372982/0444722c-bd22-4fe7-b58a-8696ca5df7e1)

This version of the ‘live’ form view now shows the form creator that they are seeing “Form metrics for the past 7 days: 25 September to 2 October 2023”.  

There is a paragraph at the start of this section telling the form creator the limitations of the data shown:  
> If you want to track metrics over a longer period you'll need to make a note of these on the same day each week. 

They are then present with 3 separate pieces of data displayed next to each other as though blocks.  

The first box shows “Completion rate” with the figure “75%” beneath it.  

The second box shows “Forms submitted” with the figure “4” beneath it. 

The third box shows “Forms started but not completed” with the figure “1” beneath it.  

### Live form view where there is no metrics data available within the last week

![Live form view where there is no metrics data available within the last week. Screenshot](https://github.com/alphagov/forms/assets/35372982/dc87926f-09bc-4f89-8c65-c7d011b8d6d2)

This version of the screen introduces a section where the form has been live for more than 7 days but there were no submissions.  

The section heading has changed to “Form metrics for the past 7 days: 25 September to 2 October 2023”.   
Within this section form creators are presented with inset text telling them:  

> No metrics are available as no-one has started or submitted a form in the past 7 days.  
> This may be because the form is no longer published on GOV.UK.  

### Live form view where there is a problem getting metrics from CloudWatch

![Live form view showing “Sorry, there's a problem getting your form's metrics. Try again later”. Screenshot](https://github.com/alphagov/forms/assets/35372982/1b0ac6f9-e643-4682-b24c-5f4583e48f43)

This version of the screen shows there has been an error with the data storage (CloudWatch) or the system was unable to get the data requested.  

This would only appear where there has been a server request error.  

___

<br>

## Research

[Plan and run UR on data dashboard / analytics needs](https://trello.com/c/dwNKBIev/1054-plan-and-run-ur-on-data-dashboard-analytics-needs)  

We have currently not tested the design implementation with users but our researcher has done a preliminary round of research with current partners to understand: 

- How are users getting on with the current data they receive from our performance analyst?
- What data are they using the most? And for what purpose?
- Are they sharing or tracking data in any way, and how?
- Are there any needs or trends that we can see that would be impacted by our initial agreed MVP?

[Notes: Data and Analytics needs (Google document)](https://docs.google.com/document/d/1Tz417kZuXHz_PFYOxkQk0_EdvoUt4SvvGEwJ5zZefP0/edit?usp=sharing)  
[Playback - Form data and analytics (Google deck)](https://docs.google.com/presentation/d/1sOhNmWa1Cih22l6FZ5FQCdDwPKMb4WS_PzkCSFd2HH4/edit?usp=sharing)  
[Research playback: Data & Analytics (Recording)](https://drive.google.com/file/d/1cKwbV6u9iV3EecFvHIfjsbYcBgHdDC6x/view?usp=sharing)  

<br>

___

<br>

[Back to the top](#metrics-for-form-creators-v1)
