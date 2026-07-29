# Kinjuson

Kinjuson is a lightweight browser app for building structured forms in JSON.

It now works as a split editor:
- the left side is a visual form builder
- the right side is a read-only live preview of the interactive form
- JSON remains the canonical draft format
- the editor can load and save JSON and export a self-contained HTML file

The exported HTML file embeds the form JSON in the document and includes the runtime needed to use the form without any extra files.

## What You Can Do

- create a new blank form
- load the bundled example
- load an existing JSON file
- edit form metadata and author-only AI task instructions
- add, describe, rename, reorder, and remove sections, subsections, and questions
- preview the form without changing answers in the preview pane
- track completion progress at a glance in the preview
- save the current draft as JSON
- export the current draft as a standalone HTML form
- save progress from an exported form back into a new standalone HTML file
- export completed responses as JSON or table-based Markdown

## How To Use It

1. Open `index.html` in your browser.
2. Choose one of these starting points:
   - `New blank`
   - `Load example`
   - `Load`
3. Build the form in the left panel.
4. Use the read-only live preview on the right to check the result and monitor completion progress.
5. Watch the `Saved` or `Unsaved` indicator and click `Save changes` to download the current JSON draft.
6. Click `Export HTML` when you want a single self-contained form file.

## Generated HTML

The exported HTML file:
- contains the interactive form markup
- embeds the JSON definition inside the file
- can be opened directly in a browser
- preserves subsection descriptions, question states, notes, labels, theme color, and the `checked` compatibility field
- shows when progress has changed since the last HTML save
- provides `Save progress` to download the current form state as HTML
- provides `Export` with `JSON` and `Markdown` items
- includes the author-defined task in JSON and Markdown exports without displaying it in the form UI

The Markdown export is intended for passing a completed response to an AI agent or tool. It includes the task, respondent details, completion information, subsection descriptions, notes, and every answer. It does not calculate or export evaluative scores. Sections use numbered level-one headings, subsections use numbered level-two headings, and each subsection has its own table with the description above it and notes below it.

## JSON Structure

Kinjuson uses a v1 JSON structure:

```json
{
  "app": "Kinjuson",
  "version": 1,
  "form": {
    "title": "Website Launch Readiness",
    "description": "A simple example form for checking whether a website is ready to launch.",
    "task": "Review the completed form, summarize the main blockers, and recommend the next actions.",
    "themeColor": "#1d6fd6",
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
          "description": "Review the readiness and approval status of the primary website pages.",
          "note": "Homepage is done, pricing page still needs legal review.",
          "questions": [
            {
              "text": "Homepage copy is final",
              "state": "yes",
              "checked": true
            }
          ]
        }
      ]
    }
  ]
}
```

## Fields

### Top Level

- `app`: app name
- `version`: format version
- `form`: form metadata shown in the header and top fields
- `sections`: list of form sections

### `form`

- `title`: header title shown at the top of the form
- `description`: header subtitle
- `task`: author-only multiline instructions included in JSON and Markdown exports but hidden from the preview and respondent form
- `themeColor`: accent color used by the form
- `nameLabel`: label for the name field
- `namePlaceholder`: placeholder for the name field
- `name`: value of the name field
- `dateLabel`: label for the date field
- `date`: value of the date field in `YYYY-MM-DD` format

### `sections`

Each section contains:
- `id`: automatically generated positional section identifier
- `title`: section title
- `subsections`: list of subsections

Each subsection contains:
- `title`: subsection title
- `description`: author guidance shown below the subsection title and above its questions
- `note`: free-text comment
- `questions`: list of questions

Each question can be:
- a simple string
- or an object with `text` and answer state data

Supported answer states:
- `unset`
- `yes`
- `no`

For backward compatibility, exported files also include `checked`.

## Example Form

- Example JSON file: [form_example.json](form_example.json)

## Typical Use Cases

- project audits
- launch readiness checks
- team health reviews
- internal assessments
- process evaluations
- structured decision support
- AI-assisted reporting from structured assessment data
