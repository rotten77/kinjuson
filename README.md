# Kinjuson

Kinjuson is a lightweight browser app for working with structured forms defined in JSON.

It is useful when you want to:
- define goals, structured assessments, checklists, or question sets
- fill them in manually in a simple UI
- save your work and continue later
- reuse the same app for many different kinds of analysis by changing only the JSON template
- produce structured output that can be analyzed later by people or AI

The app uses JSON as both the input template and the saved output format.

**Its main purpose is to help you collect structured data first, and then use that data for analysis, summaries, reporting, or AI-assisted evaluation. Instead of manually rewriting your findings into a report, you can export the JSON result and pass it to an AI tool to generate a report from it.**

## What The App Does

Kinjuson loads a JSON file and renders it as an interactive form.

The form can contain:
- header metadata such as title, description, labels, and dates
- sections and subsections
- questions
- notes for each subsection

For each question, the app supports three answer states:
- `unset`
- `yes`
- `no`

While filling the form, the app:
- tracks progress
- calculates section and overall scores
- lets you add notes
- exports the current state back to JSON

The result is a JSON file that captures the full structure and current answers. That exported file can be used as:
- a saved snapshot of progress
- a machine-readable input for later processing
- source material for AI-generated reports, summaries, recommendations, or analysis

## How To Use It

1. Open `index.html` in your browser.
2. Click `Import JSON`.
3. Select a JSON template or a previously saved form.
4. Fill in the form:
   - enter the top-level fields
   - choose `Unset`, `Yes`, or `No` for each question
   - add notes where needed
5. Review the summary and section scores.
6. Click `Export JSON` to save your current progress.
7. Later, import the exported JSON file to continue where you left off.

You can also take the exported JSON and use it with AI to:
- generate a report
- summarize findings
- identify weak areas or gaps
- suggest actions based on the answers

## JSON Structure

The app expects a JSON object with:
- optional app metadata
- a `form` object
- a `sections` array

### Main Structure

```json
{
  "app": "Kinjuson",
  "version": 1,
  "form": {
    "title": "Website Launch Readiness",
    "description": "Machine structures, human inputs",
    "nameLabel": "Project",
    "namePlaceholder": "Enter project name...",
    "name": "Marketing Site Refresh",
    "dateLabel": "Review date",
    "date": "2026-03-26"
  },
  "sections": [
    {
      "id": "1",
      "title": "Content",
      "subsections": [
        {
          "title": "Core pages",
          "note": "Homepage is done, pricing page still needs review.",
          "questions": [
            {
              "text": "Homepage copy is final",
              "state": "yes",
              "checked": true
            },
            {
              "text": "Pricing page has been approved",
              "state": "no",
              "checked": false
            },
            {
              "text": "Contact page includes current team details",
              "state": "unset",
              "checked": false
            }
          ]
        }
      ]
    }
  ]
}
```

## Field Description

### Top Level

- `app`: app name
- `version`: format version
- `form`: form metadata shown in the header and top bar
- `sections`: list of form sections

### `form`

- `title`: header title shown at the top of the page
- `description`: header subtitle
- `nameLabel`: label for the first text field
- `namePlaceholder`: placeholder for the first text field
- `name`: current value of the first text field
- `dateLabel`: label for the date field
- `date`: current value of the date field in `YYYY-MM-DD` format

### `sections`

Each section contains:
- `id`: section identifier
- `title`: section title
- `subsections`: list of subsections

Each subsection contains:
- `title`: subsection title
- `note`: free-text comment
- `questions`: list of questions

Each question can be:
- a simple string
- or an object with `text` and answer state data

Example question object:

```json
{
  "text": "Forms submit successfully",
  "state": "yes",
  "checked": true
}
```

## Answer States

The current app works with three explicit states:
- `unset`: not answered yet
- `yes`: positive answer
- `no`: negative answer

For backward compatibility, exported files also include `checked`.

## Example Form

- Example generic form: [form_example.json](/c:/Users/zatloukal/Documents/dev/sqa-kickstart-framework/app_audit/form_example.json)


## Typical Use Cases

- project audits
- launch readiness checks
- team health reviews
- internal assessments
- process evaluations
- structured decision support
- AI-assisted reporting from structured assessment data
