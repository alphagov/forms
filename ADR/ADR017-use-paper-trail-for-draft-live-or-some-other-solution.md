# ADR017: Use Papertrail for draft/live or some other solution

Date: 2023-03-03

## Status

Rejected

## Context

GOV.UK Forms needs a way to "snapshot" forms and any other associations to be used as a live form. A form could potentially 
have multiple "live" forms during its lifetime but only one live form should be accessible at any given time. 

Using [PaperTrail](https://github.com/paper-trail-gem/paper_trail) already creates an audit record of a form/pages record 
and stores the object in its previous state. It however only works on a model by model basis with no built-in way
of recording which version a parent record was when an association record was create/updated or deleted.

PaperTrail does have a 3rd party  [associations](https://github.com/paper-trail-gem/paper_trail#4b-associations) plugin 
called [paper_trail-associations_tracking (PT-AT)](https://github.com/westonganger/paper_trail-association_tracking) which 
we tried as part of a spike.

This gem should be able to give us the functionality we needed such as trying to identify which versions of pages make 
up a specific version of the form.

### Positives
- PT-AT can identify which forms/pages where created/updated and it was possible to restore them again to serve up to our form filler users.
- PT allows custom events so a new event for "make live" could be used to identify specific live versions.
- Keep audit of events and records together in one table.

### Negatives
- We cannot safely delete pages and be able to retrieve the specific live form which may have used that delete page. 
  PT-AT doesn't work well when deleting associations such as pages and it was found that `.length/size/count` after delete
  didn't return the expected number of pages for a form as it seemed to query the pages table rather than version table
- PT-AT contributor recommends not using PT-AT because of its dependency on PT and its "blackbox" approach which doesn't seem
  right to just assume everything works.
- There are a lot of [limitations](https://github.com/westonganger/paper_trail-association_tracking#limitations) and [known issues](https://github.com/westonganger/paper_trail-association_tracking#known-issues).
  One such issue that we came across "Not compatible with transactional tests" which made it extremely hard if not possible
  to test any data we were expecting.

The PT-AT gem states the following as alternative solution

> Model Versioning and Restoration require concious thought, design, and understanding. You should understand your versioning and restoration process completely. Because PT-AT it is mostly a blackbox solution which encourages you to set it up and then assume its "Just Working". This can make for major data problems later.
>
> Instead I recommend a newer gem that I have created for handling snapshots of records and associations called [active_snapshot](https://github.com/westonganger/active_snapshot). This gem does not utilize paper_trail at all. The focus of this gem is to have a simple and fully understandable design is easy to customize and know inside and out for your projects needs.

We did briefly investigate using active_snapshot but there were a couple of issues and concerns we had about using it

- This suggestion was made over 2 years ago by the author of PT-AT which is why they are recommending it. Looking at downloads
  from RubyGem.org (at this time, theres been a total of 18,858 downloads of which 1893 where for the current version 0.3.0).
  This seems rather low given the time period and also not main blog posts/mentions of it online.
- We would have to use this in addition to papertrail as it isn't automatically integrated into ActiveRecord create,update,delete

## Decision

The team decided not to use PT-AT or active_snapshot to implement draft/live versions and to keep papertrail strictly for auditing/versions.

## Consequences

Given the issues discovered and the complexity around this, we created our own implementation of snapshotting
forms and pages. We created a new table called `made_live_forms` which stores the json version of the form and its pages
as a JSON column. This is simpler to understand what is happening and gives us flexibility of adding new features to
it in the future.
