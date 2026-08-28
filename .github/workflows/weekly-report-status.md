---
name: Weekly Report Status
description: Publish a concise weekly activity report for commits, issues, and pull requests.
engine: copilot
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
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

Create one concise activity report for the previous seven full days, ending at
the workflow run start time in UTC. Use GitHub data to cover:

- Commits pushed to this repository
- Issues opened, closed, or otherwise substantially updated
- Pull requests opened, closed, merged, or otherwise substantially updated

Publish the report as a new issue using the `create-issue` safe output. Include
the UTC reporting window and links or numbers for the relevant activity. State
clearly that there was no activity when all three categories are empty; still
publish the issue in that case. Do not create more than one issue.