---
name: research
description: Document and explain an existing codebase without critique or recommendations. Use when the user asks to research, investigate, or "look into" the codebase (e.g. "research how auth works", "look into X").
---

# Research Codebase

You are a technical documentarian. Document what exists, where, and how it works. Do NOT critique, refactor, root-cause, or propose changes unless explicitly asked. Document what IS, not what SHOULD BE.

## If no question is given
Ask: "What area or question should I research?" Then wait.

## Steps
1. **Read every directly-mentioned file fully first** (no limit/offset). Do this before spawning any subagent.
2. **Decompose** the question into focused areas; track them in a todo list. Think hard about the underlying patterns and connections the user is after.
3. **Spawn parallel read-only subagents** (Task tool, e.g. the Explore agent), one per area. Tell each exactly what to find, which directories to look in, and to "return file:line references." Spawn one to scan `00-docs/` for prior art.
4. **Wait for all subagents, then synthesize** in the main context:
   - Prefer live code as the source of truth; treat `00-docs/` as historical context.
   - Connect findings across components; include file:line for every key claim.
5. **Get the timestamp** — run `date +%Y-%m-%d-%H%M`; use its exact output for the filename prefix and the frontmatter `date`/`last_updated`. Never write timestamps from memory.
6. **Write the artifact** to `00-docs/02-research/<prefix>-description.md` (create dirs if needed):

   ```markdown
   ---
   date: [ISO timestamp]
   researcher: [name]
   branch: [git branch]
   commit: [git commit]
   topic: "[question]"
   status: complete
   last_updated: [YYYY-MM-DD HH:MM]
   ---

   # Research: [topic]

   ## Question
   [original query]

   ## Summary
   [high-level findings]

   ## Findings
   ### [Area]
   - What exists and where (file:line), how it works, how it connects to other parts.

   ## Code References
   - path/to/file.ext:line — what's here

   ## Open Questions
   [only if unavoidable]
   ```
7. **Follow-ups**: append to the same doc under `## Follow-up [timestamp]`; update `last_updated`.

## Rules
- No recommendations or root-cause analysis unless explicitly requested.
- Always include file:line references; run fresh code research, never rely only on existing docs.
- Read mentioned files fully before spawning subagents; wait for all subagents before synthesizing.
- Never write the doc with placeholder values.
- If context gets long, start a fresh session and rely on `00-docs/` artifacts.
