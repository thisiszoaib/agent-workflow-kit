# agent-workflow-kit

Shared [Cursor](https://cursor.com) / agent workflow for Angular projects: one entrypoint (`AGENTS.md`), engineering standards (`docs/standards/`), and task skills (`.agents/skills/`).

## Layout

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Agent entrypoint — where to look for rules and skills |
| `docs/standards/` | Implementation conventions (architecture, components, stores, testing, …) |
| `.agents/skills/` | Task-triggered capabilities (code review, NgRx store, Material theming, …) |
| `AGENTS.local.md` | **Your project only** — exceptions; not copied or overwritten by the kit |

Code review lives in the **code-review** skill only, not in `docs/standards/`. Topic standards own audit rules; the skill orchestrates scope, routing, and report format.

## Install into a project

From GitHub (before npm publish):

```bash
npx github:thisiszoaib/agent-workflow-kit init
```

From npm (after publish):

```bash
npx agent-workflow-kit init
# or
npx agent-workflow-kit init
```

Target another directory:

```bash
npx agent-workflow-kit init ./path/to/my-app
```

Skip overwriting files that already exist (default for `init`):

```bash
npx agent-workflow-kit init
```

Overwrite on install:

```bash
npx agent-workflow-kit init --force
```

## Commands

| Command | Description |
|---------|-------------|
| `init [dir]` | Copy `AGENTS.md`, `docs/standards/`, `.agents/skills/` into the project |
| `update [dir]` | Refresh managed files from the kit (overwrites by default) |
| `list` | Show kit version, managed paths, standards, and skills |
| `doctor [dir]` | Verify managed paths exist in the project |

```bash
npx agent-workflow-kit update          # refresh standards + skills
npx agent-workflow-kit update --no-force   # only add missing files
npx agent-workflow-kit list
npx agent-workflow-kit doctor
```

## Local overrides

After `init`, add **`AGENTS.local.md`** at the project root for repo-specific rules (stack versions, forbidden patterns, links to internal docs). The kit never manages that file.

`AGENTS.md` already points agents at standards, skills, and local overrides.

## Manifest

Managed paths are listed in `manifest.json` for predictable updates:

```json
{
  "version": "0.1.0",
  "managedPaths": [
    "AGENTS.md",
    "docs/standards",
    ".agents/skills"
  ]
}
```

## Publishing

1. Clone from [github.com/thisiszoaib/agent-workflow-kit](https://github.com/thisiszoaib/agent-workflow-kit).
2. `npm publish --access public` (optional).
3. Consumers run `npx agent-workflow-kit init` or `npx github:thisiszoaib/agent-workflow-kit init`.

## Developing the kit

```bash
node bin/install.mjs list
node bin/install.mjs doctor ..          # check parent Angular app
node bin/install.mjs init /tmp/test-app --force
```

## Included skills

- `angular-developer` — upstream Angular patterns and references
- `angular-material-theming` — Material 3 theming and token overrides
- `angular-new-app` — new Angular CLI app guidance
- `ngrx-signal-store` — NgRx Signal Store patterns
- `code-review` — convention review workflow (orchestrates `docs/standards`)

## Included standards

- `architecture.md`, `core-engineering.md`, `angular-components.md`, `forms.md`
- `templates-and-styling.md`, `material.md`, `state-and-stores.md`
- `services-and-side-effects.md`, `testing.md`
