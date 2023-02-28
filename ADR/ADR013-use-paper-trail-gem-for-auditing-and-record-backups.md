# ADR013: Add PaperTrail gem for auditing and record backup

Date: 2023-02-27

## Status

Accepted

## Context

We need way to audit changes to database records to identify what has changed and who made those changes. This information
will be surfaced to users later on when we come to versioning. This is still valuable to record now for any support tickets
that come in and require us to understand the form/pages history.

There is also a secondary need be able to restore individual records rather than having to restore from database backups.

## Decision

Add [PaperTrail](https://github.com/paper-trail-gem/paper_trail) as part of draft/live work so we can start recording 
changes to Forms/Pages but also from any other tables we might want to monitor.

## Consequences

We will be able to identify very easily what attribute on a specific model changed, when it changed and who changed it.
This means that we do not have to trawl splunk server logs trying to see what information had been sent to the server
and at what point did the model get updated to. We also need this information to surface back to the user.

By setting it up now, we can double check the data that's being collected and tweak it before surfacing it to our users. 
If there are any issues we can reconfig or completely drop and restart this data collection without any questions from our users.

We already know that we will need to do some additional work to identify who made the changes as we don't record that now as 
forms-api does not have this data. We will need to pass it in from forms-admin. If we do setup PaperTrail now, when we 
come to do User Management, we can set up the extra details as part of that work.

### Positives

- We can identify exactly what has changed and when it was changed.
- We can restore from a specific version of Form/Page. This can be done through migration or Rails console, as a team we also
  discussed the option of building an endpoint/UI which super admins may have access to to do these sort of tasks.
- PaperTrail adds call back into all the crud actions create/update/delete so its easy to track those events
- PaperTrail also accepts custom events an can be manually triggered
- It's really easy to tell PaperTrail to track a model by including `has :papertrail` to the model that you would like to
  track. There are also additional configuration options to control if/when to log changes.
- PaperTrail is very customisable and used a lot within the Rails community for auditing/tracking 
- When we come to versioning and surfacing versions to our users we will already have some details to display

### Negatives
- Currently we don't have a means of passing users details between forms-admin and forms-runner. So we will not be able 
  to record users details straight away but we can look at configuring Papertrail to include these details as part of 
  User Management work we have planned in the future
- Difficult to link associations records together but if we record both Form/Pages, we should at least be able to restore 
  specific versions of each one if a support ticket comes in.

