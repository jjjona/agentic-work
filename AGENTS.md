## Agent Resources & Workflow

- For detailed instructions on current multi-session tasks, temporary scripts, and design tokens, please refer to: agent-resources/README.md
- **Thoughts workflow**: For multi-step or multi-session work, prefer the artifact-first workflow in `agent-resources/thoughts/` (start with `agent-resources/thoughts/README.md`).
  - Keep “thoughts” artifacts short, factual, and resumable (links to files/symbols over long dumps).
  - Do not put secrets, tokens, customer data, or other sensitive material in artifacts.
- Split up multi-step prompts into small, modular tasks and make todos for those tasks if there would be more than one todo.
- All user-visible strings must come from the project’s translation system. Do not output literal text directly.
- Check for any type, linting, or execution-errors before finishing.
- Correct those errors and keep iterating until error-free.
- Never end a session while lint/tests are failing unless the user explicitly instructs otherwise; rerun the relevant commands after each change and fix the failures you introduced before replying.

## Other project guidelines

- Put other instructions here.