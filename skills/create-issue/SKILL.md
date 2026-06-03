---
name: create-issue
description: Capture a bug report or feature request as a structured issue file under 00-docs/01-issues. Use when the user reports a problem or asks to "create an issue for ...".
---

# Create Issue

## Steps
- Confirm the issue title if it isn't explicit.
- Target dir: if `00-docs/01-issues/` exists, write there; if `00-docs/` is missing, ask where.
- Owner: use `git config --get user.name`; if empty, ask.
- Date: get it with `date +%Y-%m-%d` and use it for both `date` and `last_updated` (don't write it from memory).
- Filename: `YYYY-MM-DD-<slug>.md` (slug = lowercased ASCII title, spaces/punctuation → hyphens, collapsed).
- Fill the template below.

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

## Testing
- Unit tests:
- Manual QA steps:

## Open questions
- Q1:
```
