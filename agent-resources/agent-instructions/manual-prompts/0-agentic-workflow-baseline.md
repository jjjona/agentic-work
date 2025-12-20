# Agentic Workflow Baseline

Use a research -> plan -> implement flow by default, and keep context lean.

## Frequent Intentional Compaction
- Prefer compact artifacts (research docs, plans, progress notes) over long chat history.
- Summarize noisy tool output and only keep details needed for correctness.
- If context grows large, use the Compaction prompt to write a compact Progress Memo before proceeding.
- After writing to agent-resources/thoughts/, use the Compaction prompt to refresh the Progress Memo.

## Subtasks and Context Control
- Use separate chat sessions for parallel searching or targeted investigation to avoid polluting the main context.
- Keep subtask prompts focused and read-only; return concrete file paths and brief findings.
- Wait for all subtasks before synthesizing.

## Human Leverage
- Treat research and plans as highest leverage; assume humans will review them closely.
- Avoid speculative changes; verify in the codebase whenever possible.

## Output Discipline
- Prefer precision over verbosity.
- No slop: avoid vague filler or ungrounded claims.
