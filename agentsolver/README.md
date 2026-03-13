# agentsolver

C3 package for the AI Acceleration Assistant. Bare framework ready for the C3 Code agent to extend.

**See also:** [../docs/SCOPING.md](../docs/SCOPING.md) for full scope and [../docs/HANDOFF.md](../docs/HANDOFF.md) for handoff notes.

## Where to add what

| Purpose | Location |
|--------|----------|
| C3 types, methods, epics | `src/` |
| Pure React pages (no SDL) | `ui/c3/src/customInstances/` (e.g. `agentsolver.Dashboard.tsx`) |
| UI routes | `metadata/UiSdlRoute/` (e.g. `routes.csv`) |
| SDL page config (if needed) | `ui/c3/meta/` |
| Themes, bundler, UiSdlConfig | `config/` |
| Seed data | `seed/` |
| Tests | `test/` |
| Static assets | `ui/content/assets/` |

UI is **pure React** (no SDL) per scope; use `uiComponentLibraryReact` and custom `.tsx` in `ui/c3/src/`.
