# Class Diagrams for GOV.UK Forms apps

The mermaid files in this directory are [Class Diagrams](https://mermaid.js.org/syntax/classDiagram.html) for each of the apps we run that make up the main GOV.UK Forms system.

## How to generate

In each app, install the `rails-erd` gem:

```ruby
group :development do
  gem "rails-erd", git: "https://github.com/voormedia/rails-erd.git"
end
```

We need the latest version in the repo, as at the time of writing the most recent release does not include [Mermaid support](https://github.com/voormedia/rails-erd/commit/22cfc76098e222b7c211f0369e80580aeaa22c70).

> ⚠️ Note: Do not commit the gem into the app repos.

Run:

```shell
generator="mermaid" rake erd
```

This will create a file called `erd.mmd` in the root of the application.

## Update the diagram

1. Open the file in an editor and copy the contents (all of the `classDiagram` block).
2. Paste the contents into the corresponding diagram file, replacing everything inside the "mermaid" block:
````
```mermaid
classDiagram
...
```
````
3. Update the date near the top of the file.
