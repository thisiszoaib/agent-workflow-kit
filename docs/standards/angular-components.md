# Angular components

Project policy for components and templates. Generic Angular patterns: `[.agents/skills/angular-developer/SKILL.md](../../.agents/skills/angular-developer/SKILL.md)`.

## Architecture

This section is **Angular app shape** (standalone, routes, signals). For `**src/app` folder roles** (core / features / shared) and layering, see [architecture.md](architecture.md).

- Prefer standalone components over NgModules.
- Do **not** set `standalone: true` in decorators (default in Angular v20+).
- Use signals for state management; use `computed()` for derived state.
- Implement lazy loading for feature routes.
- Do **not** use `@HostBinding` or `@HostListener`. Put host bindings in the `host` object of `@Component` or `@Directive`.

## Components

- Keep components small and focused on a single responsibility.
- Use `input()` and `output()` instead of decorators.
- Set `changeDetection: ChangeDetectionStrategy.OnPush`.
- Prefer **inline templates** (`template: \`...`). External` templateUrl` should be rare; if used, keep paths relative to the component TS file.
- Do **not** use `ngClass`—use `class` bindings.
- Do **not** use `ngStyle`—use `style` bindings.
- For external styles (e.g. Material theming SCSS), use paths relative to the component TS file.

## Images

- Use `NgOptimizedImage` for static images.
- `NgOptimizedImage` does not work for inline base64 images.

## Templates

- Keep templates simple; avoid complex logic.
- Use native control flow (`@if`, `@for`, `@switch`) instead of `*ngIf`, `*ngFor`, `*ngSwitch`.
- Use the async pipe for observables.
- Do not assume globals like `new Date()` are available in templates.
- Do not use arrow functions in templates (not supported).

See also: [templates-and-styling.md](templates-and-styling.md), [material.md](material.md), [forms.md](forms.md).