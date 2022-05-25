# ADRTBD: Use DFE-Digital component based libraries to build runner frontend

Date: 2022-05-24

## Status

Proposed

## Context

We need to use the GOV.UK design system to display forms to form-completers. The frontend must meet the accessibility and browser support standards set out in the [service manual](https://www.gov.uk/service-manual/technology/designing-for-different-browsers-and-devices).

As the design system doesn't offer it's own Ruby library we are faced with the choice of using a community option or implementing our own using the tools available in ruby/rails.

Implementing our own components based on the design system would require us to
track changes, develop and test the components we need. This approach
offers the most flexibility but also requires the most effort.

The following projects package the design system frontend in a format we could consume in Rails.

They vary in goals, implementation and completeness.

- [GOV.UK Publishing components](https://github.com/alphagov/govuk_publishing_components)
- [DFE-Digital Rails ViewComponents]( https://github.com/DFE-Digital/govuk-formbuilder)
- [DFE-Digital Rails ViewComponent for Forms](https://github.com/DFE-Digital/govuk-components)
- [The DXW GOV.UK Frontend for Rails](https://github.com/dxw/dxw_govuk_frontend_rails)

The publish components are used by GOVUK to build the citizen facing and admin
UI of the GOVUK publishing platform. They include many more components than the standard design system.

The DXW components are less complete and are not kept up to date with same frequency as the other options.

## Decision

Of the above libraries the DFE-digital projects are the most suitable.
- they closely track the latest GOVUK Frontend system
- they are well tested, maintained and used in lots of projects
- are based on [ViewComponents](https://github.com/github/view_component) which strong testing locale and preview support

 For our project they give us a way to add new page/field components in an encapsulated, easy to test and modify way.

## Consequences
 - need to keep the GOVUK assets - CSS/JS etc tracking the same release as the DFE components, which don't include assets.
 - need to pin version in Gemfile ad track updates manually.
