---
description: Adds a dated daily update and accessible confirmation dialog to the site.
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
engine: copilot
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

Add the current daily update to `index.html`.

## Date

Use the workflow run's UTC date, not the local timezone or a date inferred from repository history. Determine it at runtime with:

```bash
date -u +%Y-%m-%d
```

Format the date using the existing wording convention in the page, such as `1st of August`, including the correct ordinal suffix and full month name. Use the same normalized date when deriving any new element IDs.

## Editing requirements

- Inspect `index.html` before editing.
- Add the UTC date to the existing `Daily Updates` navigation using the same button structure, classes, arrow treatment, and date wording already present.
- Add one matching native `<dialog>` for the new update, following the existing dialog structure, classes, ID conventions, accessible labeling, close control, and styling hooks.
- The dialog must confirm that the daily update for the UTC date ran successfully.
- Connect the navigation control to the dialog with `aria-haspopup="dialog"`, `aria-controls`, and the existing `data-dialog-trigger` convention.
- Do not modify `styles.css` or any file other than `index.html`.
- Preserve every existing daily update and all existing page content.
- Before editing, check whether the UTC date is already represented by a navigation control and matching dialog. If it is already present, make no change and do not create a pull request.
- Do not duplicate a date, navigation control, or dialog.

If a change is needed, create exactly one pull request using the configured safe output. Keep the change limited to the new dated navigation item and its matching dialog.