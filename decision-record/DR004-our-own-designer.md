# DR004: Develop our own GOV.UK Forms "designer" for private beta

Date: 2022-02-24

## Status

Accepted

## Context

We're deciding what "designer" interface to use to support our first private beta partner to create a form. We're considering two goals:

1. When we last met with our CEO, Tom Read, on 20 December 2021, we discussed some goals for getting existing document-based forms on GOV.UK starting to use online forms
2. While we don't have a set deadline, Tom Read is curious what we can ship early that is small, but visible and high impact

Having tested the [XGovFormBuilder](https://github.com/XGovFormBuilder/digital-form-builder) with Civil Servants that create document-based forms, we saw early signs in four out of five tests, they could create online forms that were better than document-based forms, meeting our definition of "good enough". We also saw there were no major accessibility issues after testing with someone with low vision and one blind person.

However, there were many aspects of XGovFormBuilder that slowed users down, and prevented users from realising their intended designs. While they were "good enough", the forms they created would have been better if the creators had been able to achieve what they were trying to do.

If we used the XGovFormBuilder with our first private beta partner, as long as we provided a similar level of guidance and tutorials, we could expect similar results to the alpha tests, and would learn how it works with real forms rather than fictional tasks we give users.

However, beyond our first partnership, we believe achieving our goal of a self-service platform that meets the needs of form creators would require significant changes to the XGovFormBuilder. From initial design and technology explorations in alpha, we believe making those changes to an existing codebase would take longer than developing our own "designer" interface that would initially be aimed at tackling very basic forms, then iteratively adding in features to allow users to tackle forms with more complex features.

## Decision

We're going to develop our own GOV.UK Forms "designer" for private beta, as long as we're able to do the following:

1. Following our alpha service assessment, we need to identify a realistic path to our first private beta partner being able to create their own basic forms as soon as possible
2. Following our alpha service assessment, we need to identify a realistic path to publishing our first form as soon as possible, considering partner organisations' lead times
3. Currently, our sponsors are supportive of our timelines — potential users are still patient and there's not a current threat to our funding, though there's always a need to prove the value of our work early on

If we need to publish forms faster, we will need to see how we could use XGovFormBuilder as the "designer" with our first private beta partner, making sure we can easily migrate the forms to our own platform, which we would develop in parallel.

## Consequences

Following our alpha assessment, we will develop our own GOV.UK Forms "designer", building on both learnings from testing XGovFormBuilder and design explorations around a [wizard with an on-page preview](https://forms-prototypes.london.cloudapps.digital/form-designer/form-index).

Working with our first private beta partner, we will try to define the simplest possible "designer" as part of the wider platform. We'll be defining the [GOV.UK Forms "skateboard"](https://app.mural.co/t/gaap0347/m/gaap0347/1645702506888/13236cfcc4b7cb126185a7b3d23ec1008d1d5587?sender=u5376ce1d3dfeb38176618793).

While we estimate there to be 259 document-based forms on GOV.UK that we could tackle with a simple feature set, we will need to show flexibility with our partners, and may need to add in some more complex features sooner if necessary.

One way of visualising our private beta roadmap may be to plot actual forms we want our users to be able to tackle at different stages of private beta.
