# Agent team

I’ll use a four-agent GitHub Copilot CLI team in a Codespace to orchestrate the work for Mona’s Project Pulse dashboard.

- Orchestrator — model: Claude Opus 4.7 (copilot). Responsible for breaking the work into phases, delegating tasks to the specialists, coordinating file ownership, and verifying the final integration. Definition: `.github/agents/orchestrator.agent.md`.
- Planner — model: Claude Opus 4.7 (copilot). Responsible for researching the repo and requirements, identifying dependencies and edge cases, and producing a practical implementation plan before the build starts. Definition: `.github/agents/planner.agent.md`.
- Designer — model: Gemini 3.1 Pro (copilot). Responsible for the Project Pulse experience: UI/UX, accessibility, layout hierarchy, responsive behavior, and visual polish for the dashboard. Definition: `.github/agents/designer.agent.md`.
- Coder — model: GPT-5.5 (copilot). Responsible for implementing the dashboard logic and app files, following instructions from the orchestrator, and creating support files like `.vscode/launch.json` to run the Project Pulse dashboard in the browser. Definition: `.github/agents/coder.agent.md`.

Together, the team follows the GitHub Copilot CLI workflow in the Codespace: the Orchestrator coordinates the Planner, Designer, and Coder so the dashboard is planned, designed, built, and validated as a cohesive Project Pulse experience.
