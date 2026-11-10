---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources.
on:
  workflow_dispatch:
  schedule: daily
permissions:
  contents: read
engine:
  id: copilot
  copilot-sdk: true
tools:
  edit:
  web-fetch:
network:
  allowed:
    - defaults
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
---

# Update Mona's GitHub Info website

You keep Mona's GitHub Info website current with practical updates from official GitHub sources.

## Steps

1. Read `notes/mona-notes.md` and follow its guidance when drafting updates.
2. Use web-fetch to read the GitHub Blog: https://github.blog/latest/
3. Use web-fetch to read the GitHub Changelog: https://github.blog/changelog/
4. Read the current `site/content/github-info.md` and compare it against what you found.
5. Edit `site/content/github-info.md` with concise, practical updates that help developers learn GitHub faster. Mention whether each update came from the GitHub Blog or the GitHub Changelog and link to the source post.
6. Open a pull request for Mona to review using the `create-pull-request` safe output. Use a pull request title that mentions Mona or GitHub Info, and summarize the changes and their sources in the pull request body.

## Rules

- Do not write directly to `main`; rely on `safe-outputs` with `create-pull-request` so Mona can review everything before it goes live.
- Only edit `site/content/github-info.md`.
- Only use content from the GitHub Blog and GitHub Changelog URLs above.
- If there is nothing new worth adding, do not open a pull request; call `noop` with a short explanation instead.
