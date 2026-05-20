# Angular Material

- Before adding or editing Material usage, check **[material.angular.dev](https://material.angular.dev)** (Components) for current template syntax.
- Prefer **directive-based** attributes from the docs (e.g. `matButton`, `matIconButton`, `matButton="filled"`) over legacy selector forms (`mat-button`, `mat-icon-button`, `mat-flat-button`).

## Theming and overrides

- Use `[.agents/skills/angular-material-theming/SKILL.md](../../.agents/skills/angular-material-theming/SKILL.md)` and `mat.<component>-overrides()` with design tokens from the docs.
- **Never** override internal Material CSS classes.

## Images

- Use `NgOptimizedImage` for static images (see [angular-components.md](angular-components.md)).

