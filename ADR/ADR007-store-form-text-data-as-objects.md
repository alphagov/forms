# ADR007: Storm form text data as objects

Date: 2022-05-26

## Status

Proposed

## Context

> the facts behind the need to make the decision

GOV.UK Forms aims to be viable for use for any form on GOV.UK with suitable transaction volume - this means that we also have to support forms that are available in more languages than just English. For example:

The Legal Aid Agency providers a number of forms in both English and Welsh:

- Form overview: https://www.gov.uk/topic/legal-aid-for-providers/forms
- Welsh specific versions: https://www.gov.uk/government/publications/asiantaeth-cymorth-cyfreithiol-ffurflenni-cymraeg-welsh-forms

Were we to replace these (or any other forms where multiple language versions are provided) with digital equivalents we have two options:

### Option 1: Do not support multiple languages per form in the runner, get users to create one form per each language


**Example schema**
```json
{
  "form": {
    "id": 1,
    "language": "en (or other language code)"
  }
}
```

With this option we could decide to offload this to our users and not support multiple languages in a single form but instead give each form a language. This would require the language to be selected up front so that the runner knows how to present the surrounding text (i.e. The text on the continue button, the titles for static pages, etc) and one form to be created per language.

The major downside of this approach would be the overhead to form creators where a form needs to be in multiple languages - every update to a forms wording must be done on multiple forms which all need sign off, any addition of any fields could very easily become out of sync with different languages without noticing and end up in a situation where only one language is the most up to date form.

Additionally, we would not be able to respect the users locale settings in their browser, instead assuming that if they would navigate to the correct form themselves.

### Option 2: Support multiple languages per form, providing translations in the schema for any user generated text:

**Example schema**
```json
{
  "form": {
      "pages": [
        {
          "questionText": {
            "en": "The title in English",
            "cy": "The title in Welsh",
            "es": "The title in Spanish"
          }
        }
      ]
  }
}
```

In this option we could choose to embed translations alongside each text entry in the form, with the form creators providing translations where appropriate for their forms. This would require the builder to allow an interface for defining these translations, and the runner to access the translation when provided for each form.

With this approach we could use the users browsers settings to decide which language to show if one is available, or provide a language picker displaying the available languages. It would enable forms to stay updated and inline across multiple languages, and we would be able to require translations to be set for forms where they need to be published in that language.

## Decision

We have decided to go with option 2, supporting multiple languages per form.

## Consequences

- The API will need to format text in this for the runner
- The runner will need to support multiple languages from day one
  - Reading from the form data by locale
  - All static content provided by the locale
- The form builder will eventually need to support adding in translations for a form
