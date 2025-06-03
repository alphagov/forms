---
title: GOV.UK Forms Admin app class diagram
---

# GOV.UK Forms Admin app class diagram
## 2025-05-29

```mermaid
classDiagram
	direction RL
	class `CreateFormService::CreateFormEvent`
	`CreateFormService::CreateFormEvent` : +integer dedup_version
	`CreateFormService::CreateFormEvent` : +integer form_id
	`CreateFormService::CreateFormEvent` : +string form_name
	class `DraftQuestion`
	`DraftQuestion` : +jsonb answer_settings
	`DraftQuestion` : +text answer_type
	`DraftQuestion` : +integer form_id
	`DraftQuestion` : +text guidance_markdown
	`DraftQuestion` : +text hint_text
	`DraftQuestion` : +boolean is_optional
	`DraftQuestion` : +boolean is_repeatable
	`DraftQuestion` : +text page_heading
	`DraftQuestion` : +integer page_id
	`DraftQuestion` : +text question_text
	class `FormSubmissionEmail`
	`FormSubmissionEmail` : +string confirmation_code
	`FormSubmissionEmail` : +string created_by_email
	`FormSubmissionEmail` : +string created_by_name
	`FormSubmissionEmail` : +integer form_id
	`FormSubmissionEmail` : +string temporary_submission_email
	`FormSubmissionEmail` : +string updated_by_email
	`FormSubmissionEmail` : +string updated_by_name
	class `Group`
	`Group` : +boolean branch_routing_enabled
	`Group` : +boolean exit_pages_enabled
	`Group` : +text external_id
	`Group` : +boolean file_upload_enabled
	`Group` : +string name
	`Group` : +string status
	class `GroupForm`
	`GroupForm` : +integer form_id
	class `Membership`
	`Membership` : +string role
	class `MouSignature`
	class `Organisation`
	`Organisation` : +string abbreviation
	`Organisation` : +boolean closed
	`Organisation` : +integer default_group_id
	`Organisation` : +string govuk_content_id
	`Organisation` : +boolean internal
	`Organisation` : +string name
	`Organisation` : +string slug
	class `PaperTrail::Version`
	`PaperTrail::Version` : +string event
	`PaperTrail::Version` : +string item_type
	`PaperTrail::Version` : +jsonb object
	`PaperTrail::Version` : +jsonb object_changes
	`PaperTrail::Version` : +string whodunnit
	class `User`
	`User` : +string app_name
	`User` : +boolean disabled
	`User` : +string email
	`User` : +boolean has_access
	`User` : +datetime last_signed_in_at
	`User` : +string name
	`User` : +string organisation_content_id
	`User` : +string organisation_slug
	`User` : +text permissions
	`User` : +string provider
	`User` : +boolean remotely_signed_out
	`User` : +string role
	`User` : +datetime terms_agreed_at
	`User` : +string uid
	`Item` --> `PaperTrail::Version`
	`Organisation` --> `PaperTrail::Version`
	`User` --> `PaperTrail::Version`
	`User` --> `CreateFormService::CreateFormEvent`
	`Group` --> `CreateFormService::CreateFormEvent`
	`Organisation` --> `User`
	`User` --> `Membership`
	`User` ..> `Group`
	`User` --> `MouSignature`
	`User` --> `DraftQuestion`
	`Organisation` --> `Group`
	`Organisation` --> `MouSignature`
	`Group` --> `Membership`
	`Group` --> `GroupForm`
  ```
