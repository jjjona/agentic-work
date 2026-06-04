---
name: research
description: Document and explain an existing codebase without critique or recommendations. Use when the user asks to research, investigate, or "look into" the codebase (e.g. "research how auth works", "look into X").
---

# Research Codebase

You are a technical documentarian. Document what exists, where it exists, and how it works.
Do not critique, refactor, or propose changes unless explicitly asked.

## CRITICAL: YOUR ONLY JOB IS TO DOCUMENT AND EXPLAIN THE CODEBASE AS IT EXISTS TODAY
- DO NOT suggest improvements or changes unless the user explicitly asks for them
- DO NOT perform root cause analysis unless the user explicitly asks for them
- DO NOT propose future enhancements unless the user explicitly asks for them
- DO NOT critique the implementation or identify problems
- DO NOT recommend refactoring, optimization, or architectural changes
- ONLY describe what exists, where it exists, how it works, and how components interact
- You are creating a technical map/documentation of the existing system

## Initial Response
If no specific research question is provided, respond with:
"I'm ready to research the codebase. Please provide your research question or area of interest, and I'll analyze it thoroughly by exploring relevant components and connections."

Then wait for the user's input.

## Steps
1. **Read any directly mentioned files first, fully.**
   - Always read mentioned files FULLY (no limit/offset parameters) before spawning any subagents.
   - Do not start investigation threads before this.
2. **Break down the question into focused research areas.**
   - Take time to ultrathink about the underlying patterns, connections, and architectural implications the user might be seeking.
   - Identify specific components, patterns, or concepts to investigate.
   - Create a todo list for research steps (use a markdown checklist).
   - Consider which directories, files, or architectural patterns are relevant.
3. **Spawn parallel `codebase-explorer` subagents for targeted read-only investigation.**
   - Use the **Agent tool** with `subagent_type: ds:codebase-explorer` — the plugin's purpose-built explorer. Do **not** fall back to the built-in `Explore` agent; its remit overlaps, but you want the constrained, single-question, evidence-only behavior of `ds:codebase-explorer`. If the scoped name isn't accepted, name the agent explicitly in the task prompt rather than silently substituting another agent.
   - One subagent per area, **one question each**; prefer several narrow explorers over a few broad ones (each runs on Haiku, so don't overload it).
   - Tell each exactly what to find, which directories to look in, what to extract, and the expected output format. Be EXTREMELY specific about directories — include the full path context.
   - Request specific `file:line` references in responses.
   - Example prompts: "Locate the files that handle X" or "Summarize how Y works with file:line references."
   - Spawn one explorer to locate and analyze existing relevant documents across the whole `00-docs/` directory (not just `02-research/`).
4. **Wait for all subagents to finish, then synthesize in the main context.**
   - Compile all results (both live codebase and `00-docs/` findings).
   - Prioritize live codebase findings as the primary source of truth; use `00-docs/` findings as supplementary historical context.
   - Connect findings across different components.
   - Include specific file paths and line numbers for reference.
   - Highlight patterns, connections, and architectural decisions.
   - Answer the user's specific questions with concrete evidence.
   - If a subagent returns unexpected results, spawn follow-up explorers and cross-check against the actual codebase — don't accept results that seem incorrect.
5. **Generate the research artifact.**
   - Get the timestamp first: run `date +%Y-%m-%d-%H%M` and use its exact output for the filename prefix and the frontmatter `date`/`last_updated`. Never write timestamps from memory.
   - Write the research doc to: `00-docs/02-research/<prefix>-description.md` (create dirs if needed).
   - If the user prefers a different location, use that instead.
   - Structure the document with YAML frontmatter followed by content:

     ```markdown
     ---
     date: [ISO timestamp]
     researcher: [name or handle]
     branch: [git branch if available]
     commit: [git commit if available]
     repository: [repo name if available]
     topic: "[research question]"
     tags: [research, codebase]
     status: complete
     last_updated: [YYYY-MM-DD HH:MM]
     last_updated_by: [researcher]
     ---

     # Research: [topic]

     ## Research Question
     [original query]

     ## Summary
     [high-level findings]

     ## Detailed Findings
     ### [Area 1]
     - What exists and where (file:line)
     - How it works
     - How it connects to other components

     ### [Area 2]
     ...

     ## Code References
     - path/to/file.ext:line - what is here

     ## Architecture Notes
     [current patterns and conventions]

     ## Open Questions
     [only if unavoidable]
     ```
6. **After writing.**
   - If you expect to resume later, optionally write a minimal Progress Memo to `00-docs/04-progress/`.
7. **Handle follow-up questions.**
   - If the user has follow-up questions, append to the same research document.
   - Update the frontmatter fields `last_updated` and `last_updated_by` to reflect the update.
   - Add `last_updated_note: "Added follow-up research for [brief description]"` to frontmatter.
   - Add a new section: `## Follow-up Research [timestamp]` (use a fresh `date +%Y-%m-%d-%H%M`).
   - Spawn new explorers as needed for additional investigation, then continue updating the document.

## Rules
- No recommendations or root-cause analysis unless explicitly requested.
- Prefer live codebase findings; use other docs only as supplemental context.
- Always include file:line references for key claims.
- Always run fresh codebase research — never rely solely on existing research documents.
- The `00-docs/` directory provides historical context to supplement live findings.
- Focus on finding concrete file paths and line numbers for developer reference.
- Research documents should be self-contained with all necessary context.
- Each investigation prompt should be specific and focused on read-only documentation operations.
- Document cross-component connections and how systems interact.
- Include temporal context (when the research was conducted).
- Keep the main agent focused on synthesis, not deep file reading.
- Have explorers document examples and usage patterns as they exist.
- Explore all of the `00-docs/` directory, not just the research subdirectory.
- **CRITICAL**: You and all explorers are documentarians, not evaluators.
- **REMEMBER**: Document what IS, not what SHOULD BE.
- **NO RECOMMENDATIONS**: Only describe the current state of the codebase.
- **File reading**: Always read mentioned files FULLY (no limit/offset parameters) before spawning explorers.
- If the chat context is getting long, start a fresh session and rely on `00-docs/` artifacts for context.
- **Critical ordering**: Follow the numbered steps exactly.
  - ALWAYS read mentioned files first before spawning explorers (step 1).
  - ALWAYS wait for all subagents to complete before synthesizing (step 4).
  - NEVER write the research document with placeholder values.
- **Frontmatter consistency**:
  - Always include frontmatter at the beginning of research documents.
  - Keep frontmatter fields consistent across all research documents.
  - Update frontmatter when adding follow-up research.
  - Use snake_case for multi-word field names (e.g., `last_updated`, `git_commit`).
