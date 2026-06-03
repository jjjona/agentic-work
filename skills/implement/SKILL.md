---
name: implement
description: Implement an approved plan from 00-docs/03-plans — execute phases in order and verify success criteria. Use when the user asks to implement, execute, or follow a plan, or says "start phase X", "continue with the plan", "continue with phase X".
---

# Implement Plan

Execute an approved plan from `00-docs/03-plans`. Follow the plan's intent, adapt to reality, keep progress visible.

## Start
- If no plan path is given, ask for one.
- Read the plan fully, plus the ticket and every file it references (no limit/offset — you need full context).
- Note existing `- [x]` checkmarks; resume from the first unchecked item and trust completed work.
- Build a todo list from the phases.

## Execute
- Implement each phase fully before the next; stay within the plan's scope.
- Check off items in the plan file as you complete them.
- If reality doesn't match the plan, STOP and surface it:
  ```
  Issue in Phase [N]:
  Expected: [what the plan says]
  Found: [actual situation]
  Why it matters: [explanation]
  How should I proceed?
  ```

## Verify each phase
- Run the automated success criteria; fix failures before moving on.
- Then pause for human verification:
  ```
  Phase [N] complete — ready for manual verification.
  Automated checks passed:
  - [list]
  Please verify manually:
  - [manual items from the plan]
  Tell me when done so I can start Phase [N+1].
  ```
- Don't check off manual items until the user confirms.
- If told to run multiple phases consecutively, skip the pause until the last one.

## Rules
- Read files fully; don't expand scope beyond the plan.
- If context gets long, start a fresh session and rely on `00-docs/` artifacts (and the plan's checkmarks) to resume.
- Optionally update a progress memo in `00-docs/04-progress/` if you'll resume later.
