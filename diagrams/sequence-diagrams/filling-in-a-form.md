# Filling in a form

```mermaid 
sequenceDiagram
  actor user as Form filler
  participant govuk as GOV.UK website
  participant runner as forms-runner
  participant api as forms-api
  participant notify as GOV.UK Notify
  participant inbox as shared email inbox
  actor processor as Form processor

```