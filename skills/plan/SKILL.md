---
name: plan
description: Create a detailed, testable, phased implementation plan through research and iteration. Use when the user asks to plan, create a plan, or wants a structured plan before coding.
---

# Create Plan

Produce a detailed, testable, phased implementation plan. Be skeptical, thorough, and collaborative. Work interactively — don't dump a full plan in one shot; get buy-in at each step.

## If no task is given
Ask for the task description, constraints, and any relevant docs. Then wait.

## Process

### 1. Gather context
- Read all mentioned files fully (no limit/offset).
- Spawn read-only subagents (Task tool) to locate relevant code/patterns and to scan `00-docs/` for related work; read what they surface in the main context.
- Summarize current state. Ask ONLY questions you genuinely cannot answer from code or `00-docs/`:
  ```
  Based on the ticket and my research, we need to [accurate summary].
  Found:
  - [detail with file:line]
  - [pattern / constraint]
  Questions I couldn't answer from code:
  - [needs human judgment]
  ```

### 2. Verify & explore
- If the user corrects you, don't just accept it — verify against the actual files before proceeding.
- Find conventions, integration points, dependencies, tests, and examples; return file:line refs.
- Present design options with trade-offs and agree on a direction.
- Resolve every open question before writing the plan.

### 3. Agree on structure
Propose the phase breakdown (name + what each accomplishes) and get feedback before writing details.

### 4. Write the plan
Get the prefix by running `date +%Y-%m-%d-%H%M` (use its exact output — never write the timestamp from memory). Write to `00-docs/03-plans/<prefix>-[ticket-]description.md` (kebab-case description, ticket id optional). Template:

````markdown
# [Task] Implementation Plan

## Overview
[What we're implementing and why]

## Current State
[What exists now, what's missing, key constraints — with file:line]

## Desired End State
[Spec of the end state and how to verify it]

## What We're NOT Doing
[Explicit out-of-scope items, to prevent scope creep]

## Approach
[High-level strategy and reasoning]

## Phase 1: [Name]
### Changes
**File**: `path/to/file`
[Summary + specific code to add or modify]

### Success Criteria
**Automated:**
- [ ] Tests pass: `<cmd>`
- [ ] Lint / typecheck pass: `<cmd>`
**Manual:**
- [ ] [Human-verified behavior]

After automated checks pass, pause for human confirmation of manual testing before the next phase.

## Phase 2: [Name]
[Same structure]

## References
- Ticket: `00-docs/01-issues/...`
- Research: `00-docs/02-research/...`
````

### 5. Review & iterate
Share the path; ask whether phases are scoped right and success criteria are specific enough. Refine until the user is satisfied.

## Rules
- Be skeptical: question vague requirements, verify with code, don't assume.
- Be interactive: buy-in at each step, allow course corrections.
- Read context files fully before planning; include file:line refs throughout.
- **No open questions in the final plan** — resolve or ask before writing. Every decision made up front.
- Always split success criteria into **Automated** (commands an agent can run) and **Manual** (human testing).
- Always include a "What we're NOT doing" section.
- If context gets long, start a fresh session and rely on `00-docs/` artifacts.
