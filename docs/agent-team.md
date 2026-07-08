# Agent team

This repository defines a small custom agent team to build Mona's Project Pulse dashboard.

- Orchestrator — model: Claude Opus 4.7. Coordinates Planner, Coder, and Designer; breaks requests into phases and assigns explicit file scopes. Definition: .github/agents/orchestrator.agent.md

- Planner — model: Claude Opus 4.7. Creates research-backed implementation plans, lists file assignments, dependencies, and validation expectations. Definition: .github/agents/planner.agent.md

- Coder — model: GPT-5.5 (copilot). Implements code changes, fixes bugs, and provides runnable app support (Project Pulse launch configuration). Definition: .github/agents/coder.agent.md

- Designer — model: Gemini 3.1 Pro (copilot). Handles UI/UX, accessibility, information architecture, and visual styling for the dashboard. Definition: .github/agents/designer.agent.md

Work is coordinated from a Codespace using the GitHub Copilot CLI. Follow the Orchestrator's delegation rules; do not stage/commit/push changes unless explicitly instructed by the learner.
