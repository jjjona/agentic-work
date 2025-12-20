---
name: Compaction (Thoughts)
description: Write a compact progress memo to reset context safely.
argument-hint: Summarize the current state and write the progress memo.
target: vscode
---
# Compact Progress (Roo Code)

Rewrite the current working set into a minimal, correct Progress Memo.
This is used to reset context when it grows large or after producing artifacts.

## Trigger Conditions
- After writing to agent-resources/thoughts/
- When the chat context is getting long or noisy

## Inputs
- The current conversation (or a summary)
- Any key artifacts (plan/research/progress)

## Compaction Rules
- Prefer fewer, higher-confidence facts.
- Explicitly mark assumptions and unknowns.
- Drop raw logs; keep only minimal error summaries.

## Output Location
- Write the Progress Memo to: agent-resources/thoughts/progress/YYYY-MM-DD-HHMM-<slug>--resume-memo.md
- If agent-resources/thoughts/ does not exist, create it.
- If the user provides a different progress path, use that instead.

## Output (Required)
- Goal
- Current hypothesis/approach
- Key code locations
- What's done (verified vs unverified)
- What's next (smallest action)
- Open questions / risks

## Stop Condition
Stop when the memo is small enough to paste into a fresh session and continue without re-reading the transcript.
