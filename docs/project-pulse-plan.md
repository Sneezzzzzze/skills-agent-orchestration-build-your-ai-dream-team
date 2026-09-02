# Project Pulse implementation plan

## Summary

Project Pulse is a lightweight static dashboard that helps Mona's team quickly understand the status of active projects, ownership, recent activity, priority, and contributor-friendly summaries. This plan uses the GitHub Copilot CLI in a Codespace to orchestrate work through the custom agent team: the Orchestrator coordinates the workflow, the Planner defines execution phases, the Designer shapes the UX and visual system, and the Coder implements the actual static app and preview configuration.

## Goal

Build a small, polished dashboard that renders project information from a local JSON dataset and opens cleanly from a VS Code launch configuration named "Run Project Pulse Dashboard". The dashboard should feel like an executive snapshot, not a placeholder page, and it should be easy to validate without additional setup.

## Implementation phases

### Phase 1: Define the data contract and file ownership

- Confirm the project data shape in `app/project-data.json`.
- Use a top-level `projects` array with each project including the fields required by the brief: `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Keep the data contract simple and deterministic so the front-end can render it without extra transformation logic.

File assignments:
- `app/project-data.json` — Coder
- Orchestrator oversight — confirms the requirements and final scope before implementation begins

Dependencies:
- This step must finish before the HTML and CSS can be finalized, because both will rely on the known fields and the project count.

### Phase 2: Design the dashboard experience

- Create a polished layout with a strong title, consistent spacing, clear typography, status badges, and project cards.
- Ensure the structure supports quick scanning: project name, owner, status, recent activity, and priority should all be visually distinct.
- Use deterministic styling hooks such as `.dashboard` and `.project-card`, plus visual affordances like rounded corners, shadows, spacing, and contrast.
- Keep the experience accessible and readable on a typical laptop viewport while still feeling complete and intentional.

File assignments:
- `app/styles.css` — Designer lead
- `app/index.html` — Designer provides layout structure, Coder implements final markup details

Dependencies:
- The design should be informed by the data model in `app/project-data.json` and the content structure in `app/index.html`.
- The Designer and Coder should align on project-card semantics before final styling is locked.

### Phase 3: Build the dashboard markup and data binding

- Create `app/index.html` with the required "Project Pulse" title and a dashboard container.
- Reference the stylesheet and JSON data from the page so the app is rendered as a self-contained static dashboard.
- Render project cards in a structured way using the dataset from `app/project-data.json`.
- Keep the page lightweight and static; no framework is required.

File assignments:
- `app/index.html` — Coder
- `app/project-data.json` — Coder
- `app/styles.css` — Designer review and approval

Dependencies:
- `app/project-data.json` must exist before the HTML can consume it reliably.
- `app/styles.css` should be in place before the final rendering review so the layout can be checked visually.

### Phase 4: Add the preview launch configuration

- Create `.vscode/launch.json` for the dashboard preview.
- Use the required launch name: "Run Project Pulse Dashboard".
- Set the launch configuration to run from the `app/` directory and open `index.html` directly so the learner sees the dashboard instead of a directory listing.
- Keep the configuration deterministic and easy to run in Codespaces or VS Code.

File assignments:
- `.vscode/launch.json` — Coder
- Designer review — confirms the launch behaves like a real dashboard preview, not a directory listing

Dependencies:
- This step depends on the final `app/index.html` and related file structure being stable.
- It should be created last so its configuration matches the completed dashboard layout and file names.

## Designer and Coder responsibilities

### Designer

- Guides the dashboard information hierarchy and interaction flow.
- Defines the visual treatment: spacing, typography, contrast, status badges, project-card rhythm, and the polished "Project Pulse" first impression.
- Reviews `app/index.html` and `app/styles.css` for usability and visual clarity.
- Ensures the dashboard reads as a contributor-friendly project overview rather than a generic HTML page.

### Coder

- Implements the static dashboard structure and data integration.
- Creates the project dataset in `app/project-data.json` and the HTML skeleton in `app/index.html`.
- Writes the launch configuration in `.vscode/launch.json` to preview the app.
- Validates that the files load correctly and that the launch configuration opens the dashboard instead of the folder view.

## Dependencies between tasks

1. The `app/project-data.json` contract comes first because both the HTML and CSS rely on known data fields and content structure.
2. The HTML and CSS are built together after the data model is agreed, but the final finalization depends on consistent card semantics.
3. The `.vscode/launch.json` file should be created only after the dashboard files are stabilized.
4. The Orchestrator hands off the final result only after all files are validated together.

## Parallel work decisions

- Parallel work is appropriate for the Designer and Coder after the requirements are locked:
  - The Designer can draft `app/styles.css` while the Coder prepares the project data and skeletal HTML structure.
  - The Coder can work on `app/index.html` while the Designer iterates on the layout styling, as long as the card naming and structure remain aligned.
- Sequential work is required for the launch configuration because it depends on the final file paths and app structure.
- The Orchestrator should avoid broad overlap between the HTML and CSS once the first iteration is approved, because styling changes may require markup adjustments.

## Validation expectations

The plan should be considered successful when all of the following are true:

- `app/index.html` contains the exact title "Project Pulse" and references `styles.css` and `project-data.json`.
- `app/styles.css` includes a `.dashboard` selector and a `.project-card` pattern that supports the dashboard layout.
- `app/project-data.json` is valid JSON and contains a top-level `projects` array with the expected fields.
- `.vscode/launch.json` exists and includes the launch configuration name "Run Project Pulse Dashboard".
- The dashboard opens from the app directory and shows the project cards, status badges, and priority summaries instead of a directory listing.
- The final page is readable, polished, and aligned with the dashboard brief.

## Open questions

- None blocking at this stage; the brief is specific enough to proceed without extra discovery.
- If additional project details are desired later, the data file can be expanded, but the current plan keeps the initial version intentionally lightweight and testable.
