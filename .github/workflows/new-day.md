---
name: New Day
description: Add the current UTC date to the site's daily updates.
engine: copilot
on:
  # schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit:
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

Update the site's daily updates for the workflow run's current UTC date.

1. Set `RUN_DATE` to the workflow run's UTC calendar date using `date -u +%Y-%m-%d`.
2. Read `index.html` and determine the existing date wording and ID conventions from its daily updates navigation and dialogs. Convert `RUN_DATE` to the matching ordinal wording used by the page, such as `1st of August`.
3. If `RUN_DATE` is already present in `index.html`, make no change and finish without creating a pull request.
4. Otherwise, edit only `index.html`:
   - Add one navigation control for the date to the existing `Daily Updates` navigation.
   - Add one matching accessible `<dialog>` using the existing structure, IDs, ARIA attributes, classes, wording style, and date conventions. The dialog must confirm that the daily update ran for the UTC date.
   - Preserve every existing daily update and do not duplicate any date, navigation control, or dialog.
   - Do not modify `styles.css` or any other file.
5. Create at most one pull request with the `create-pull-request` safe output only when `index.html` changed. The pull request must contain no file other than `index.html`.
