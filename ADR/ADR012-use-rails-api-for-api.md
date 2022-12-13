# ADR012: Use Rails-API for api (Replacing ruby-grape)

Date: 2022-12-12

## Status

Accepted

## Context

Currently, form-api is written using ruby-grape (originally it also included Sinatra which was later removed). 
The reasons for using ruby-grape has become unclear over time other than possibly being a lighter framework than Ruby on Rails. 
However as most of developers on the team are not Ruby developers, it does make it harder
for developers to familiarise themselves with not just one framework (Ruby on Rails) but two different ones (ruby-grape)
making it hard to context switch and to follow conventions used between the two frameworks. 

It also makes it harder to follow patterns through the three repositories when some ruby gems require libraries like ActiveRecord.

We been looking at how we can build a draft/live feature for forms and there are pretty standardised ways of doing this
without having to rebuild it. One such way is using a gem called paper-trail but it does require ActiveRecord.  It has 
a lot of extra features that we know will be needed in the future like showing what has changed between various various
and it also allows us to audit all our database tables for any creations, updates and deletions (and offers database record recovery)

## Issues already identify and fixed 

- DB Connection maxing out because the app was not setup properly to terminate connections on error (Error handling)
  https://github.com/alphagov/forms-api/pull/70
- DB Memory leak discovered because every request was not tidying up after itself
  https://github.com/alphagov/forms-api/pull/98
- The difficulty we faced implementing features such as question reordering and making forms live. Lack of a solid model over the Forms and Pages meant adding these features took longer than necessary.

Potential future problems we may face
- DB recovery from failed deployments. How to do this in grape/Sequal. Rails already does this well out the box and is well
  documented
 
### Option 1 - Implement ActiveRecord into ruby-grape

This may work at first and get over the initial hurdle but then when you start adding more gems they may rely on other gems
that aren't included and before long its case of fire fighting weird bugs, limitations and attempting to rebuild Ruby on Rails.

### Option 2 - Implement our own draft/live version feature

Creating proprietary software is not always ideal as it can be costly to maintain and would not be as feature rich and 
battle tested like other open source software. Again it would be fairly easy to implement at first but would soon be missing
out on vital features.

Team members would still have to understand grape and having to learn two very frameworks

### Option 3 - Switch to using Rails API
GDS recommends Rails API https://docs.publishing.service.gov.uk/manual/conventions-for-rails-applications.html#use-api_only-mode-for-api-projects

Rails advantages over Grape
- wider adaption so there is more documentation available and better integration with other products and services. This results in less work for the development team
- more commonly used in GDS, so we would enable re-use of other projects code and make it easier for GDS developers to offer help and support our project
- easier to find developers familiar with Rails than grape/sequel
- our existing Rails developers, have extensive experience using ActiveRecord and or little prior experience using the sequel ORM
- allow us to reuse more of the existing work across our three projects, reducing the maintenance cost
- allow us to implement new features faster as we will have a more structured base to build off
- reduces the time needed to onboard new developers, as the three projects have a shared framework

## Decision

The team have decided to go with option 3 as appears to have more benefits for the team, product and brings us closer inline with the rest of GDS

## Consequences

- Developers only have to learn and understand one ruby framework. We dont not have to rebuild and solve problems that
have already been answered, free us up to work on more complicated matters that are for our users.
- The migration to Rails will take time and could potentially introduce bugs or other issues. This is mitigated by the introduction of tests. It is expected that that the time spent migrating will be outweighed by the increased speed with which new features can be added and less time spent on maintainence.
- moving to Rails will give us more options to implement the draft/live feature. As well as existing libraries such as [papertrail](https://github.com/paper-trail-gem/paper_trail), [logidize](https://github.com/palkan/logidze) or [chronomodel](https://github.com/ifad/chronomodel) Rails also offers us a much stronger base to extend our current data model to include draft/live versions of forms if we were to decide to not use an existing solution.






