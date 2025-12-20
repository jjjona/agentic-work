# agentic-work
Agentic workflow for inclusion in brownfield projects, based on Dex Horthy's talk https://www.youtube.com/watch?v=rmvDxxNubIg

## What's Included

- Roo Code workflow files: custom instructions and mode definitions for the Roo Code extension.
- Copilot workflow files: repository-level custom instructions and custom agents for VS Code Copilot.
- Manual prompts: standalone Markdown prompts for use in any chat-based LLM.

## Thoughts System

This workflow relies on a lightweight "thoughts" artifact system that keeps long-running work organized and reviewable. Agents are instructed to write durable artifacts under `agent-resources/thoughts/` instead of relying on chat history.

Expected folders and files created by the workflow:

- `agent-resources/thoughts/research/YYYY-MM-DD-HHMM-description.md` for research artifacts.
- `agent-resources/thoughts/plans/YYYY-MM-DD-HHMM-ENG-XXXX-description.md` for implementation plans.
- `agent-resources/thoughts/progress/YYYY-MM-DD-HHMM-<slug>.md` for compact progress memos.

## Usage

### Roo Code
Copy the files inside the `roo-code` folder into your project root to add the custom Roo instructions and modes.

### GitHub Copilot
Copy the entire `.github` folder into your project root to add Copilot custom instructions and agents.

### Manual Mode
Use the Markdown files in `manual-prompts` as copy/paste prompts in any chat LLM.

The usual flow is to first reseach, then plan and then implement.
To get started simply choose the Research mode/agent/prompt and go from there.
Resuming work later in the process is easily done by picking the mode/agent/prompt most appropriate for where you left off.