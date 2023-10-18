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

![Live form view with no metrics available. Screenshot](https://github.com/alphagov/forms/assets/35372982/5ddfaa3a-3a02-43df-b58a-8c4cf39d6664)  
*caption*  

### Live form view with less than 7 days of metrics data

![Live form view with 3 days of metrics data. Screenshot](https://github.com/alphagov/forms/assets/35372982/8ea09690-ed56-4777-9c1c-2798659d54c3)  
*caption*  

### Live form view with 7 days of metrics data

![Live form view with 7 days of metrics data. Screenshot](https://github.com/alphagov/forms/assets/35372982/54daa06f-9d4b-4dd2-8bc6-8cdab508af92)  
*caption*

### Live form view where there is no metrics data available within the last week

![Live form view where there is no metrics data available within the last week. Screenshot](https://github.com/alphagov/forms/assets/35372982/c391a5df-93eb-4098-a3eb-38218fb72ac2)  
*caption*  

### Live form view where there is a problem getting metrics from CloudWatch

![Live form view showing there is a problem with this service. Try again later. Screenshot](https://github.com/alphagov/forms/assets/35372982/affbba5a-9864-4eb7-b322-19d42b521402)    
*caption*  


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

- 
___

<br>

## Research focus

### Things we plan to focus on in testing:
- 

<br>

___

<br>

[Back to the top](#metrics-for-form-creators-v1)
