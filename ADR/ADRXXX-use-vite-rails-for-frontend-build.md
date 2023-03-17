# ADRxxx: Use Vite and the vite_rails gem for our frontend build

Date: 2023-03-17

## Status

Accepted

## Context
Currently our frontend build is using:
- [Gulp](https://gulpjs.com/) as as task runner
- [Rollup](https://rollupjs.org/) to bundle our JS
- [Dart Sass](https://sass-lang.com/dart-sass) and [PostCSS](https://postcss.org/) to process our stylesheets
- [Sprockets](https://github.com/rails/sprockets) as our asset manager
- The [cssbundling-rails](https://github.com/rails/cssbundling-rails) and [jsbundling-rails](https://github.com/rails/jsbundling-rails) gems to pass our generated JS and CSS to Sprockets

As well as being somewhat convoluted, this build configuration also has some issues which could slow down frontend development:
- No hot module reloading (HMR) - when a change is made to the frontend code, the whole build gets re-run, and the changes aren't visible on the page until the developer manually refreshes. Build systems which support HMR will only update the modules which have changed, and apply these changes in the browser automatically.
- Relatively slow startup time - when starting the dev server, all the code is bundled and this takes time.
- The cssbundling-rails and jsbundling-rails gems both depend on [Yarn](https://yarnpkg.com/), an alternative Node package manager, rather than NPM. This means new developers have an additional global dependency to install and manage.

So far on the project these haven't been huge problems, because we're still in private beta and we haven't done much custom frontend - we've been implementing our UI with standard design system components. As our project grows and we add more features, our UI is likely to require more custom components, so we'll be writing more CSS and Javascript.

[Vite](https://vitejs.dev/) is a modern build tool which supports hot module reloading by default. It also provides a unique feature - when running the dev server it loads the source files directly on demand as [ES Modules](https://nodejs.org/api/esm.html#introduction),rather than bundling them, which makes startup time significantly quicker. It also comes with a sensible default configuration for building JS with Rollup and SCSS with Dart Sass and PostCSS, so we don't have to manage as much of this ourselves.

Vite can do many of the things we currently use Sprockets for - namely cache invalidation and manifest generation. Because of this, Sprockets is probably unnecessary for our use case. We can use [vite_rails](https://github.com/ElMassimo/vite_ruby/tree/main/vite_rails) to replace the other Sprockets features (integration with the Rails assets tasks and tag helpers for .erb files).

### Ecosystem concerns
- Vite is quite popular now - it has roughly as much usage as Gulp in the most recent State of JS survey, but unlike Gulp it's increasing in popularity.
- It's part of the Vue ecosystem, so it has a reasonably large developer community attached to it and we should be able to expect it to remain active for a while.
- Because it's ultimately using Rollup for bundling, if it does end up out of support in the future, we could move back to Rollup and Sprockets (or Propshaft) without too much trouble.

## Decision

We have decided to move from Gulp/Rollup/Sprockets and the Rails CSS/JSBundling gems to a build based on vite-rails.

## Consequences

- Faster frontend builds and updates - starting the dev server should be quicker, as should updates when code changes.
- Faster builds overall - from local testing it appears that a clean install should be quicker, because we don't need to install as many gems or Yarn.
- It's theoretically possible to for the dev server to do something different from the prod build - this is most likely to happen when devloping for browser-specific bugs. In these cases this can be circumvented by running a full build of the assets and then starting a local rails server, rather than using the vite dev server.
