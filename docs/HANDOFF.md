# Handoff for C3 Code / Genesis agent

You’re taking over from here. This repo has:

- **Scoping:** [SCOPING.md](SCOPING.md) — notes, Jira/Confluence (read-only + drafts), C3/Genesis deployment, CLI, heartbeat.
- **Package:** `agentsolver` (manifest `agentsolver/agentsolver.c3pkg.json`), platform 8.9, `uiComponentLibraryReact` 8.9.
- **Bare layout:** `src/`, `metadata/`, `config/`, `seed/`, `test/`, `ui/c3/meta/`, `ui/c3/src/`, `ui/content/assets/`.

**Suggested order to build (from SCOPING §9):**

1. Notes layer (file-based or C3-backed), tags, retrieval.
2. Confluence read + draft content for user to paste.
3. Agent + tools (notes, Jira/Confluence search, C3 docs, drafts); deploy on Genesis.
4. Build on C3 Code / Genesis (repo → build → deploy).
5. CLI as thin client to the deployed agent.
6. Heartbeat (scheduled digest).
7. Prototypes (C3 + React in adjacent repos).
8. Optional local web app calling the agent.

**UI:** Pure React only (no SDL). Add pages under `agentsolver/ui/c3/src/customInstances/` and wire routes in `metadata/UiSdlRoute/`.
