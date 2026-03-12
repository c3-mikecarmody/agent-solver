# AI Acceleration Assistant — Scoping Doc

Single source of truth for the agent/tool that supports SE + de facto TPM work (AI Acceleration + broader). Solo use.

---

## 1. Notes & content

| Aspect | Decision |
|-------|----------|
| **Who creates notes** | Only you. Agent writes in two cases: (1) when you say “save this,” (2) when the agent summarizes context into a note on your behalf. |
| **Granularity** | Per **topic** and per **discussion**. One note per topic/discussion. |
| **Structure** | **Lots of tags**; strong **retrieval** (“get me everything about X”); **graph** for connections (topics ↔ notes, related notes). |
| **External sources** | No migration. Must **source from** Confluence (and Jira). Agent **drafts** Confluence-ready content for you to paste/publish; no direct write to Confluence in v1. |

---

## 2. Scope & users

- **Scope:** Both AI Acceleration and all SE/TPM work.
- **User:** Solo (you only).

---

## 3. Jira & Confluence

| System | v1 behavior |
|--------|-------------|
| **Jira** | Read-only (search, read, summarize). Scope = whatever you have access to. |
| **Confluence** | Read-only (search, source). **Drafts:** agent produces Confluence-ready drafts for you to paste over; no direct create/update of pages in v1. Scope = whatever you have access to. |

Projects/spaces: TBD (use whatever you have access to).

---

## 4. C3

- **Products/versions:** Use **latest** across the board for docs/search (e.g. C3 Agentic AI Platform, GenAI — latest tags in C3 MCP).
- **Prototypes:** Both C3 types/transforms **and** React UI. **No SDL**; **pure React** only.
- **Location:** Prototypes live in **adjacent folders** to Agent-Solver, each with **its own repo**. Parent layout: add a repo (or multiple repos) alongside this one; prototypes are separate repos next to Agent-Solver.

---

## 5. Unblocking

- **Patterns to support:** “How do I X in C3?”, “What’s the status of Y?”, “What did we decide about Z?” — plus more as we go.
- **Sources:** Jira, Confluence, C3 docs. No Slack/internal wikis/shared drives in v1.

---

## 6. Interface & runtime

| Priority | Interface | Notes |
|----------|------------|-------|
| **Primary** | **CLI** | Main way to interact. Not tied to Cursor; usable standalone. Can be a thin client that calls the deployed agent. |
| **Secondary** | **Small local web app** | Runs locally; nice-to-have. Can also call the deployed agent. |
| **Runtime** | **Deploy on C3** so the assistant has **real access** (C3 resources, Jira/Confluence, docs). Prefer **C3 agent (Genesis)** as the engine; repo-based build on **C3 Code / Genesis**. See [§10 Deployment](#10-deployment). |

---

## 7. Proactive behavior & heartbeat

- **Proactive from day one:** Agent should proactively suggest or summarize (e.g. after you log a note, or when you open the CLI).
- **Heartbeat is important:** Periodic run (daily or configurable) for digest, “what’s new,” or reminders — not only on-demand.

---

## 8. Out of scope / deferred

- SDL for prototypes (React only).
- Jira write (create/update issues).
- Other knowledge sources (Slack, wikis, shared drives) in v1.
- C3 Community search until we see a need.
- Multi-user or shared notes.

---

## 9. Implied build order (for when we build)

1. **Repo:** Create repo for the assistant; structure for agent + tools + (optional) CLI.
2. **Notes layer:** File-based or C3-backed notes (per topic/discussion), tags, retrieval, then graph (backlinks + optional explicit links).
3. **Confluence:** Read (source) + draft Confluence-ready content for you to paste over (no direct create/update in v1).
4. **Agent + tools:** Define agent (Genesis), custom tools (notes, Jira/Confluence search, C3 docs, drafts). Deploy on C3 via Genesis so it has real access.
5. **Build on C3 Code / Genesis:** Register repo/branch, build pipeline, deploy agent from repo.
6. **CLI:** Thin client (primary interface) that calls the deployed agent (log note, search notes, ask question).
7. **Heartbeat:** Scheduled run (digest / proactive summary) — agent or separate job on C3.
8. **Prototypes:** Subagent or CLI command to generate C3 + React prototypes in adjacent repos.
9. **Local web app:** Optional UI for notes/search/dashboard, calling deployed agent.

---

## 10. Deployment

**Goal:** Deploy the assistant on C3 so it has **real access** (C3 cluster, Jira, Confluence, C3 docs, internal APIs). Use a **repo** and have it **build on C3 Code / Genesis**.

**Two deployment patterns on C3:**

| Option | What it is | Fit |
|--------|------------|-----|
| **Genesis (GenAI) agent** | Deploy as a **conversational agent** with custom tools (Python). Repo holds agent config, prompts, tool definitions. Build/deploy via Genesis (Store & Deploy). Agent runs on C3, has real access; CLI / web app call the agent API. | Best fit for “C3 agent” preference and for notes + search + draft + unblocking (agent with tools). |
| **C3 application (Release Management)** | Repo with a **C3 package** (types, services, optional React UI). Build via Release Management, deploy as an application. Good if the assistant is primarily a React app + C3 backend (notes store, search services). | Fit if you want the “brain” to be a traditional C3 app (services + UI) rather than a chat agent. |

**Recommendation:** **Genesis agent** as the core. The assistant is naturally agent-shaped (notes, search, draft, answer questions). Repo → agent definition + custom tools (notes read/write, Jira/Confluence read, C3 docs, draft generation) → build/deploy on Genesis. **CLI and local web app** are thin clients that talk to the deployed agent. Heartbeat can be a scheduled invocation of the agent or a small C3 job. This gives you real access on C3 and the option to use the C3 agent from anywhere (CLI, local app, or in-product chat).

**Local vs deployed:** The **brain runs on C3** (deployed). Local = CLI and optional web app only; they just call the deployed agent. No need to run the full stack locally for “real access.”

---

*Last updated: 2025-03-12*
