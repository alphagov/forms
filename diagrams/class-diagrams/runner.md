---
title: GOV.UK Forms Runner app class diagram
---

# GOV.UK Forms Runner app class diagram
## 2025-05-29

```mermaid
classDiagram
	direction RL
	class `Submission`
	`Submission` : +jsonb answers
	`Submission` : +jsonb form_document
	`Submission` : +integer form_id
	`Submission` : +string mail_message_id
	`Submission` : +string mail_status
	`Submission` : +string mode
	`Submission` : +string reference
	`Submission` : +datetime sent_at
  ```
