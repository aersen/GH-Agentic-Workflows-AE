---
description: Adds an unused GitHub Agentic Workflows FAQ highlight to today's daily update.
on:
  schedule:
    - cron: "0 */6 * * *"
  workflow_dispatch:
engine: copilot
permissions:
  contents: read
  copilot-requests: write
network:
  allowed:
    - github.github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# Highlight of the Day

Choose and publish one unused FAQ highlight in `index.html`.

## Source and date

Fetch the official GitHub Agentic Workflows FAQ from:

https://github.github.com/gh-aw/reference/faq/

Use the workflow run's UTC date, not the local timezone or a date inferred from repository history. Determine it at runtime with:

```bash
date -u +%Y-%m-%d
```

Format the date using the existing wording convention in the page, such as `1st of August`, including the correct ordinal suffix and full month name. Use the same normalized date when deriving any new element IDs.

## Editing requirements

- Inspect `index.html` before editing.
- Parse the fetched FAQ and select exactly one question whose question and answer are not already represented by any existing daily update in `index.html`.
- Do not invent FAQ content. Write a concise, accurate answer faithful to the official FAQ.
- Use the selected FAQ question as the new dialog heading and place the concise answer in its matching answer paragraph.
- If today's UTC date already has a placeholder dialog without an FAQ, reuse that navigation control and dialog, preserving its IDs and structure.
- Otherwise, add one matching control to the existing `Daily Updates` navigation and one matching native `<dialog>`, following the existing button structure, classes, arrow treatment, ID conventions, accessible labeling, close control, and styling hooks.
- Connect any new navigation control to its dialog with `aria-haspopup="dialog"`, `aria-controls`, and the existing `data-dialog-trigger` convention.
- Use the date in the dialog header with the existing `Daily Update / <date>` wording.
- Do not modify `styles.css` or any file other than `index.html`.
- Preserve every existing daily update and all other page content.
- Never duplicate a date, navigation control, dialog, or FAQ. If today's dialog already contains an FAQ, make no change.
- If no unused FAQ remains after comparing against all existing updates, make no change and do not create a pull request.

If a change is needed, create exactly one pull request using the configured safe output. Keep the patch limited to `index.html`.