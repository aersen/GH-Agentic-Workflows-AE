---
description: Weekly activity report summarizing commits, issues, and pull requests from the previous seven days.
on:
  schedule:
    - cron: "0 9 * * 1"  # Every Monday at 9AM UTC
  workflow_dispatch:
engine: copilot
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

## Task

Generate a concise activity report for the previous 7 full days ending at workflow start (UTC). Cover:

- **Commits** pushed to the default branch
- **Issues** opened and closed
- **Pull requests** opened, merged, and closed

Use `gh` commands (via the GitHub tools) to gather this data for the repository.

## Report Requirements

- State the exact date window covered (UTC) at the top of the report.
- Summarize each category (commits, issues, pull requests) with concise counts and highlights.
- If there was no activity in a category, or no activity at all during the window, state this clearly and explicitly — do not omit the section or leave it ambiguous.
- Keep the report concise; use `###` for section headings.
- Link to relevant commits, issues, and pull requests where useful.

## Safe Outputs

- Publish the report as a new issue using the configured `create-issue` safe output. The title should summarize the report (the `[weekly-report] ` prefix is added automatically).
- Only one issue should be created per run.
