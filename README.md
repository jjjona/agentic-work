This project contains a lightweight, artifact-first agentic workflow for brownfield projects, based on Dex Horthy's talk https://www.youtube.com/watch?v=rmvDxxNubIg

The talk is fast and dense, you might want to watch it twice :)

I updated the workflow to be skill-based because skills are an open standard and are now supported by most AI coding tools without extra setup.

## How This Is Meant To Be Used

This workflow is built around following ideas:

1) Durable artifacts are created by AI and live in the repo (`00-docs/`), so work is resumable without chat history.
2) Skills are loaded only when needed, keeping context clean.
3) The goal is to keep contexts as clean and lean as possible because filled up contexts will significantly affect generated code. The more stuff is in your context, the less usefull the AI's output will be.

### The core flow (iterate as needed)

1. Research the codebase (targeted, evidence-based)
2. Turn research into a detailed plan (make decisions here)
3. Execute the plan phase-by-phase (small, verified steps)

Each step can take multiple passes. Spend the time on research and planning, the time you spend here is magnified in the results.

Good research + a good plan = good code.
Bad plan = exponential pain during implementation.

### Keep context clean

Between major steps, start a new conversation and anchor the next step on artifacts.
Example: "Let's plan the changes from `00-docs/research/2026-01-24-1530-auth-flow.md`".

### Why skills help

- The agent can see a short list of available skills (name + description)
- The full instructions for a skill are not loaded until the skill is invoked
- Skills can be invoked implicitly (by asking in a way that matches the description) or explicitly (depending on the tool)
- This keeps skill instructions out of the context until you need them.

Examples that should naturally trigger the included skills:

- Research: "Research the codebase for how authentication works"
- Plan: "Create a detailed plan to change [current problem I have], use the research in file `00-docs/research/...`"
- Implement: "Implement phase 1 of the plan in file `00-docs/plans/...`"

`create-issue-rpi` is optional. I sometimes use it to describe a bug report or small feature request and then use that as base for the research step. Example: "Create an issue for the following bug: A user reported issues while trying to fill out form x. Field y should be populated by [some endpoint] but returned 500. Check following locations ..."

## Skills

This repo ships reusable skills under `skills/`. Skills are an open standard supported by multiple agent systems.

You can install these skills either:

- Per-project (checked into the repo)
- Per-user (in your home directory)

### Roo Code (VS Code extension)

Roo loads skills from:

- Project: `.roo/skills/<skill-name>/SKILL.md`
- Personal: `~/.roo/skills/<skill-name>/SKILL.md`

### GitHub Copilot (coding agent / Copilot CLI)

Copilot supports skills in:

- Project: `.github/skills/<skill-name>/SKILL.md`
- Personal: `~/.copilot/skills/<skill-name>/SKILL.md`

Important: Agent Skills are currently experimental, enable setting `chat.useAgentSkills` in the settings.

### OpenCode CLI

OpenCode loads skills from:

- Project: `.opencode/skills/<skill-name>/SKILL.md` (also supports `.claude/skills/...`)
- Personal: `~/.config/opencode/skills/<skill-name>/SKILL.md` (also supports `~/.claude/skills/...`)

### Codex CLI

Codex loads skills from:

- Project: `.codex/skills/<skill-name>/SKILL.md`
- Personal: `~/.codex/skills/<skill-name>/SKILL.md`

Restart Codex after adding skills.

### Claude Code

Claude Code loads skills from:

- Project: `.claude/skills/<skill-name>/SKILL.md`
- Personal: `~/.claude/skills/<skill-name>/SKILL.md`

## Installing These Repo Skills

This repository keeps the canonical skill definitions in `skills/`.
To install, copy (or symlink) each skill folder into the appropriate tool directory above.
