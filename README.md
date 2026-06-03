# agentic-work — the `ds` Claude Code plugin

An artifact-first **Research → Plan → Implement** workflow for Claude Code, packaged as the `ds` plugin (skills invoked as `/ds:research`, `/ds:plan`, …).

## Why

1. **Durable artifacts live in the repo** (`00-docs/`), so work is resumable without chat history.
2. **Skills load only when needed**, keeping context lean — and lean context means better output.
3. Spend your effort on research and planning; that effort is magnified during implementation.

> Good research + a good plan = good code. A bad plan = exponential pain during implementation.

## Install (Claude Code plugin)

```
/plugin marketplace add https://github.com/jjjona/agentic-work
/plugin install ds@ds-tools
```

## Skills

| Skill | Use it when |
|-------|-------------|
| `/ds:research` | "Research how authentication works" — documents the current codebase, no changes. |
| `/ds:plan` | "Create a plan to do X, using `00-docs/02-research/...`" — interactive, phased, testable plan. |
| `/ds:implement` | "Implement phase 1 of `00-docs/03-plans/...`" — executes a phase and verifies it. |
| `/ds:create-issue` | "Create an issue for this bug ..." — captures a structured issue brief. |

Skills trigger implicitly from how you phrase the request, or explicitly as `/ds:research`, `/ds:plan`, etc.

## The loop (iterate as needed)

1. **Research** the codebase (targeted, evidence-based) → `00-docs/02-research/`
2. **Plan** from that research (make all decisions here) → `00-docs/03-plans/`
3. **Implement** the plan phase-by-phase (small, verified steps)

Between major steps, **start a fresh session** and anchor on the artifact, e.g.
"Plan the changes from `00-docs/02-research/2026-01-24-1530-auth-flow.md`."
Each step may take several passes, so iterate.

`/ds:create-issue` is optional; use it to capture a bug or feature first, then feed it into research.

## Artifacts (`00-docs/`)

Created in your target project at runtime (the plugin does not ship them):

- `00-docs/01-issues/` — issue briefs
- `00-docs/02-research/` — current-state writeups
- `00-docs/03-plans/` — phased, testable plans
- `00-docs/04-progress/` — short memos to resume work later
