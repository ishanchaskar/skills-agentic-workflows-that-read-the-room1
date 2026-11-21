---
name: update-github-info
description: Propose practical GitHub Info updates from official GitHub Blog sources.
intent: Keep the GitHub Info page current with useful, accurately sourced guidance for developers.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    max: 1
    base-branch: main
    draft: false
    fallback-as-issue: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md`. Then use `web-fetch` to read:

- https://github.blog/latest/
- https://github.blog/changelog/

Update `site/content/github-info.md` only with verified, useful information from these official sources that helps developers learn GitHub faster. Keep summaries short and practical, preserve the page's editorial angle, and include a source link whenever information comes from the Blog or Changelog. Do not invent details or repeat information already covered.

If there is no worthwhile new information, either source cannot be fetched, or the evidence is insufficient, make no changes and call `noop` with a brief reason.

When you make a meaningful update, open exactly one non-draft pull request against `main` for Mona to review. Address the PR summary to Mona, explain the page update, and include links to the sources. Do not merge the PR or modify any other file.
