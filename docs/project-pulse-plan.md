# Project Pulse implementation plan

## Goal

Build a small, static Project Pulse dashboard that helps Mona's contributors quickly see project names, owners, current status, recent activity, priorities or risks, and short contributor-friendly summaries. The finished page should have a polished, responsive card layout and be previewable through the **Run Project Pulse Dashboard** VS Code launch configuration.

## Responsibilities and file assignments

| Owner | Assigned files | Responsibilities |
| --- | --- | --- |
| Designer | `app/styles.css` | Define the visual hierarchy, responsive layout, accessible contrast and focus treatments, typography, spacing, status and priority cues, and polished project-card styling. Coordinate class names and visual states with the Coder; include the `.dashboard` and `.project-card` hooks, rounded corners, and shadows. |
| Coder | `app/project-data.json` | Create representative project records under a top-level `projects` array. Each record includes `name`, `owner`, `status`, `recentActivity`, and `priority`, with accurate, concise contributor-facing values. |
| Coder | `app/index.html` | Build the semantic dashboard structure, use the exact page title **Project Pulse**, link `styles.css`, load `project-data.json`, and render a visible `.project-card` for each project with its status, recent activity, and priority. Handle data-loading errors clearly and keep the page usable with accessible labels and headings. |
| Coder | `.vscode/launch.json` | Add strict JSON configuration named **Run Project Pulse Dashboard**. Run `python3 -m http.server 5500` with the working directory set to `${workspaceFolder}/app`; use `serverReadyAction` to open `http://localhost:%s/index.html` so the browser shows the dashboard rather than a directory listing. |
| Orchestrator | Integration and validation (no implementation file ownership) | Coordinate the specialists, settle the HTML/CSS hooks and data contract, check that the assigned files work together, run validation, and report the result and any limitations. |

## Dependencies

- The data schema and CSS/HTML contract must be agreed before the page is integrated: the JSON uses the required field names, and the HTML uses semantic, deterministic classes that the stylesheet can target.
- Designer can create `app/styles.css` while Coder creates `app/project-data.json` in parallel, provided they align on the planned `.dashboard` and `.project-card` hooks and status/priority treatment.
- Coder should implement `app/index.html` after the data shape and styling hooks are agreed, so it can render the real fields and match the visual design.
- Coder may prepare `.vscode/launch.json` in parallel with the app files because its server settings are independent; browser verification depends on all app files being present.
- Orchestrator integration and final validation depend on all four assigned files being complete.

## Phases and parallel work

1. **Agree on the interface.** Orchestrator confirms the required project fields, accessible page structure, CSS hooks, and the launch behavior from the brief.
2. **Build independent inputs in parallel.** Designer creates `app/styles.css`; Coder creates `app/project-data.json` and may configure `.vscode/launch.json`. Keep file ownership separate.
3. **Implement and integrate the page.** Coder creates `app/index.html` using the agreed data and class contracts. Orchestrator checks that the rendered fields and styles match.
4. **Validate sequentially.** Once all files are integrated, Orchestrator validates the JSON, page references, and launch configuration, then starts the launch configuration and confirms the browser opens the dashboard. Fix any integration issues before handoff.

## Validation expectations

- Confirm all assigned files exist: `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json`.
- Parse `app/project-data.json` and `.vscode/launch.json` as JSON. Verify the data has a top-level `projects` array and every project includes `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Check that `app/index.html` has the exact title **Project Pulse**, references `styles.css` and `project-data.json`, and renders project cards with project name, owner, status, recent activity, and priority.
- Check that `app/styles.css` provides `.dashboard` and `.project-card` styling, readable spacing, responsive behavior, accessible contrast, `border-radius`, and `box-shadow`.
- Verify the launch configuration is named **Run Project Pulse Dashboard**, serves from `app/` with `python3 -m http.server 5500`, and opens `http://localhost:%s/index.html`.
- Run **Run Project Pulse Dashboard** in VS Code and confirm the browser displays the Project Pulse UI from `app/index.html`, not a server directory listing. Stop the preview server after checking.
- Review browser console or server output for load errors; confirm data renders and the layout remains usable at a narrow viewport and with keyboard navigation.
