# Agent team

This project uses a coordinated team of custom agents—orchestrated through the GitHub Copilot CLI in a Codespace—to build Mona's Project Pulse dashboard.

## Agents

### Orchestrator
- **Model:** Claude Opus 4.7 (copilot)
- **Responsibility:** Coordinates the Planner, Coder, and Designer agents to break down complex requests into tasks, manage dependencies, run work in parallel or sequentially as appropriate, and verify the integrated result.
- **Definition:** `.github/agents/orchestrator.agent.md`

### Planner
- **Model:** Claude Opus 4.7 (copilot)
- **Responsibility:** Researches the codebase, documentation, dependencies, and edge cases to create practical implementation plans with ordered steps, file assignments, dependency mapping, and validation expectations.
- **Definition:** `.github/agents/planner.agent.md`

### Coder
- **Model:** GPT-5.5 (copilot)
- **Responsibility:** Implements code-oriented tasks with clear structure, explicit errors, and testable behavior. Writes code, fixes bugs, creates support configuration (like `.vscode/launch.json`), and validates changes before reporting completion.
- **Definition:** `.github/agents/coder.agent.md`

### Designer
- **Model:** Gemini 3.1 Pro (copilot)
- **Responsibility:** Handles UI/UX, accessibility, information architecture, interaction flow, and visual design. Creates polished dashboards with clear visual affordances, responsive layout, and accessible interactions.
- **Definition:** `.github/agents/designer.agent.md`

## Orchestration approach

The GitHub Copilot CLI in a Codespace coordinates this team by:

1. Requesting a plan from the Planner to understand scope and dependencies
2. Delegating implementation work to the Coder and Designer with explicit file scopes
3. Running tasks in parallel when file scopes don't overlap
4. Running tasks sequentially when work depends on earlier output
5. Verifying the integrated result meets the project requirements
