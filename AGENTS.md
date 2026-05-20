You are an expert in TypeScript, Angular, and scalable web application development. You write functional, maintainable, performant, and accessible code.

## Single source of truth

- **Shared defaults:** `docs/standards/` — engineering conventions and implementation rules for this stack.
- **Task capabilities:** `.agents/skills/` — triggered workflows (e.g. code review, NgRx store patterns) with references.
- **Local overrides:** `AGENTS.local.md` — project-specific exceptions (not managed by [agent-workflow-kit](https://github.com/thisiszoaib/agent-workflow-kit); create and maintain in your repo).

Follow the standards files for TypeScript, accessibility, layering, Angular components, Signal Forms, templates, Material, state/stores, services, and testing.

| Topic                                              | File                                                                                       |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Layers, folders, canonical examples**           | [docs/standards/architecture.md](docs/standards/architecture.md)                           |
| TypeScript, a11y                                   | [docs/standards/core-engineering.md](docs/standards/core-engineering.md)                   |
| Components, templates (control flow, OnPush, etc.) | [docs/standards/angular-components.md](docs/standards/angular-components.md)               |
| Signal Forms                                       | [docs/standards/forms.md](docs/standards/forms.md)                                         |
| Tailwind, large templates, button layout           | [docs/standards/templates-and-styling.md](docs/standards/templates-and-styling.md)         |
| Material, theming                                  | [docs/standards/material.md](docs/standards/material.md)                                   |
| Signals, NgRx stores, `rxMethod`, inject style     | [docs/standards/state-and-stores.md](docs/standards/state-and-stores.md)                   |
| Services, store vs component boundaries            | [docs/standards/services-and-side-effects.md](docs/standards/services-and-side-effects.md) |
| Unit + E2E testing                                 | [docs/standards/testing.md](docs/standards/testing.md)                                     |

## Upstream Angular guidance

For general Angular patterns (components, DI, routing, testing depth, signal-forms API details), use **`.agents/skills/angular-developer`** (`SKILL.md` and `references/`). The `docs/standards` files state **this repo’s** stricter or additional rules on top of that skill.

## Code review

Convention audits are orchestrated by **`.agents/skills/code-review`** — not a separate `docs/standards/code-review.md`. Topic standards own audit rules; the skill handles scope, routing, checklist, and report format.
