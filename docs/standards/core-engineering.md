# Core engineering

Project-wide TypeScript and accessibility expectations. For Angular API depth, use [`.agents/skills/angular-developer/SKILL.md`](../../.agents/skills/angular-developer/SKILL.md) and its `references/` folder.

## TypeScript

- Use strict type checking.
- Prefer type inference when the type is obvious.
- Avoid the `any` type; use `unknown` when the type is uncertain.

## Accessibility

- Changes MUST pass AXE checks.
- Follow WCAG AA minimums: focus management, color contrast, and ARIA attributes.
