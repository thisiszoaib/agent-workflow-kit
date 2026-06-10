# Templates and styling

## Tailwind

- Use **Tailwind CSS** for component layout and visual styling.
- Do **not** add a component `styles` array or `styleUrls` for custom CSS unless required for Angular Material theming (e.g. `mat.button-overrides()` in SCSS).
- Prefer Tailwind utilities in templates and host `class`; use the `!` suffix when overriding Material styles (e.g. `justify-start!`).

## Large templates: split by flow

Use when a template is too large or encodes **multiple flows** in one file (e.g. forgot-password vs sign-in vs sign-up, wizards, filters + table + export, unrelated panels).

**Required review triggers:**

- Template over ~150 lines.
- Multiple large `<section>` / dialog-screen / wizard-step regions.
- Forms combined with dense result UI (Material table, export status, pagination, empty/loading/error states).
- Two or more independently nameable workflows on one route.

**Approach:**

1. Extract each distinct flow (or coherent section) into a colocated sub-component.
2. Register **one** feature-scoped store on the **parent** only (e.g. `providers: [AuthDialogStore]` on the dialog host, not `providedIn: 'root'`).
3. Sub-components use `inject(TheSameStore)` from the parent injector—do **not** add a second provider per child.
4. Reusability is not required; prefer clarity and testability.

**Review trigger:** If a sub-component mostly forwards parent store state or actions through many `input()`/`output()` pairs, inject the parent-provided feature store instead; keep inputs only for per-instance data (e.g. the current row/group id).

**How to audit:** Identify nameable regions; grep for multiple top-level branches that are different user journeys; prefer extracting filter forms and tables when dense.

**Review assessment:** For every changed component/template where these triggers apply, include a short **Template size / split assessment** in review findings. If no split is needed, briefly state why (for example, the template is long but still one coherent workflow).

**Reference:** `shared/components/auth-dialog` (`AuthDialogComponent` + main/sign-in/sign-up/forgot children + `AuthDialogStore`).

A long file from **markup alone** can be acceptable when the view is still **one** coherent screen. If the template mixes several distinct flows, prefer sub-components + one parent-provided store.

## Button and label rows (Tailwind + Material)

- **Avoid `inline-flex`** for inner wrappers inside `matButton` (or full-width buttons with `justify-center` on the host). Prefer **`flex`** for row wrappers with `items-center`, `gap-*`, and `justify-center` so content aligns with Material’s button content box.

**Audit:** Grep `inline-flex` inside `matButton` / `<button` regions; flag unless documented exception.

## Oversized component class

If one `*.component.ts` combines a large inline template with heavy logic, introduce a colocated local `signalStore` (`providers: [XxxLocalStore]`), move business logic and async work there, and keep the component as wiring. Do not use injections that depend on the component/dialog host inside `withState` factories; share contracts via a small `*.types.ts`. For dialogs, keep `MatDialogRef` / `MAT_DIALOG_DATA` in the thin layer (store or component).

See also: [state-and-stores.md](state-and-stores.md), [angular-components.md](angular-components.md).
