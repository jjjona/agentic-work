# Agent Resources

This directory may contain optional working files specifically for AI agents collaborating on this repository. The high‑level entry point for all repository guidance remains `AGENTS.md`; this README focuses only on how to use `agent-resources/`. If the referenced folders or files are not found, they are not needed at the current time.

If you’re doing multi-step or multi-session work, prefer the artifact-first **Thoughts** workflow in `agent-resources/thoughts/`.

## Files and Folders

- `agent-resources/assets/`: Temporary helper images and visual assets used during development.
- `agent-resources/thoughts/`: Artifact-first workflow for reliable agent work in real codebases.
  - Start here: `agent-resources/thoughts/README.md`
  - Long-running work should track state in `agent-resources/thoughts/progress/`.
- `agent-resources/agent-plan.md` (optional / legacy): If present, a lightweight single-file plan.
  - Prefer `agent-resources/thoughts/` for anything beyond a quick, single-session change.
- `agent-resources/scripts/`: Temporary helper scripts used during development.
  - Use this folder for **short-lived Node.js scripts** (JavaScript only) that help analyze data, inspect the codebase, or automate repetitive tasks.
  - These scripts are not part of the production app and may be cleaned up or replaced at any time.
- `agent-resources/tmp/`: Temporary development documentation and scratch data.
  - Use this for **ephemeral artifacts** such as exported API responses, legacy system notes, or one-off experiment outputs.
  - The exact contents are expected to change frequently and may be gitignored; treat this folder as scratch space, not long-term documentation.
- `agent-resources/figma_styles_vars.json`: Centralized design tokens for Figma-driven work.
  - When syncing with Figma (via MCP or other tools), use these tokens as the **authoritative reference** for colors, spacing, and typography.
  - Prefer these values over ad-hoc hard-coded styles to keep the UI consistent.

## How Agents Should Use This Directory

1. **Start with `AGENTS.md`** to understand repository-wide guidelines and conventions.
2. From there, follow the link to this README to learn how to:

- Use `agent-resources/thoughts/` artifacts (research → plan → implement) for multi-step work.
- Store and clean up temporary scripts in `agent-resources/scripts/`.
- Use `agent-resources/tmp/` only for short-lived development documents and data.
- Align UI work with `figma_styles_vars.json`.

3. Keep this directory tidy: remove obsolete scripts and temporary files when they are no longer needed.
