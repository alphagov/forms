---
title: GOV.UK Forms Runner app class diagram
---

# GOV.UK Forms Runner app class diagram
## 2025-05-29

```mermaid
classDiagram
    direction RL
    class `Delivery`
    `Delivery` : +datetime delivered_at
    `Delivery` : +string delivery_reference
    `Delivery` : +datetime failed_at
    `Delivery` : +string failure_reason
    `Delivery` : +datetime last_attempt_at
    class `Submission`
    `Submission` : +jsonb answers
    `Submission` : +jsonb form_document
    `Submission` : +integer form_id
    `Submission` : +string mode
    `Submission` : +string reference
    `Submission` : +string submission_locale
    class `SubmissionDelivery`
    `Submission` --> `SubmissionDelivery`
    `Delivery` --> `SubmissionDelivery`
    `Submission` "0..*" -- "0..*" `Delivery`
  ```
