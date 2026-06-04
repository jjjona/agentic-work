---
name: create-issue
description: Capture a bug report or feature request as a structured issue file under 00-docs/01-issues. Use when the user reports a problem or asks to "create an issue for ...".
---

# Create Issue

## Workflow

- Detect that the user is reporting a problem or asking to create an issue (e.g. "I found these problems", "saw an issue", "these things are wrong", "create an issue for").
- Confirm or ask for the issue title if it is not explicit.
- Resolve the target directory.
  - If `00-docs/01-issues/` exists in the current project, write the issue there.
  - If `00-docs/` does not exist, ask the user where to write the issue.
- Determine the owner from git config at creation time.
  - Run `git config --get user.name` in the current repo.
  - If empty, ask the user for an owner name.
- Compute the issue date by running `date +%Y-%m-%d` (don't write it from memory); use it for both `date` and `last_updated`.
- Generate a slug from the issue title: lowercase, ASCII, replace spaces/punctuation with hyphens, collapse multiple hyphens, trim leading/trailing hyphens.
- Create the file as `YYYY-MM-DD-<slug>.md` in the target directory.
- Fill the template below, using the computed date for `date` and `last_updated`, the git user for `owner`, and the confirmed issue title.

## Template

```
---

date: YYYY-MM-DD

owner: "<name>"

repository: "<repo>"

topic: "<Issue Title> — Issue Brief"

status: draft

last_updated: YYYY-MM-DD

---

# <Issue Title> — Issue Brief

## Problem

- Current behavior:

- Pain:

- Desired outcome:

## Scope

- In scope:

- Out of scope:

## Affected areas

- Routes / screens / modules:

- Key states (loading / empty / error):

## Data / sources

- System of record:

- Read/write paths:

## Rules / validation

- R1:

- R2:

## Testing

- Unit tests:

- Manual QA steps:

## Open questions

- Q1:

- Q2:
```
