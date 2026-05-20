# State and stores

## Signals (components and general)

- Use signals for local component state; use `computed()` for derived state.
- Keep state transformations pure and predictable.
- Do **not** use `mutate` on signals; use `update` or `set`.

## NgRx Signal Store

- Prefer store properties (e.g. `store.system`, `store.components`) over `getState(store)`.
- For nested state, use **deep signals** (e.g. `store.system.color.roles()` instead of `store.system().color.roles`).
- Top-level store fields are signals you call (e.g. `store.system()`); nested properties are deep signals when available (e.g. `store.system.color.seedColor()`).

Full patterns: `[.agents/skills/ngrx-signal-store/SKILL.md](../../.agents/skills/ngrx-signal-store/SKILL.md)`.

## App-level vs local stores

**App-level** stores (e.g. `BuilderStore`, `providedIn: 'root'`) own shared business logic: Firestore, analytics, snackbar, auth, state consumed by **multiple** features/components.

App-level stores must **not** contain:

- UI state only one screen uses.
- Computeds for display strings/labels for a single dialog/panel unless genuinely shared.
- Loading flags for actions only one component triggers when a **local** `signalStore` would be clearer.

**Check:** For each `signal`/`computed`/state field: “Is this read by more than one component (or route subtree)?” If no, it does not belong in the root app store.

## Component-scoped local `signalStore`

When **one** component has lots of local state, branching flow, async work, and business logic:

1. Add a colocated `*.store.ts` (e.g. `feature-name.store.ts`) and register with `providers: [FeatureLocalStore]` on the standalone `@Component`. Do **not** use `providedIn: 'root'` unless it is a true singleton.
2. Move orchestration into `withMethods` / `withComputed`; call app-level stores and services from there, **not** from the component.
3. Component owns template, host bindings, and presentational wiring (`input()`/`output()`, thin handlers). It is fine for the file to stay long if the **template** is one coherent view; multiple flows → sub-components + shared parent store (see [templates-and-styling.md](templates-and-styling.md)).

**Examples:** Multi-step `MatDialog`s, heavy multi-mode forms. Reference: `shared/components/auth-dialog` with `AuthDialogStore` + `BuilderStore`.

## `rxMethod` vs `async`


| Use `rxMethod` when…                       | Use `async` when…                      |
| ------------------------------------------ | -------------------------------------- |
| Flow uses dialogs (`afterClosed()`)        | One-off imperative action              |
| Input tied to a signal and should auto-run | Button click with no reactive input    |
| Need `debounce`, `switchMap`, `scan`, etc. | Plain `Promise`, no stream composition |


**Violation:** Wrapping one `Promise` in `defer(() => from(promise))` with only `tap`/`catchError`/`finalize`—prefer `async`/`await` and `try`/`catch`/`finally`.

## Stores: no `effect()`

Never use `effect()` to react to signal changes in stores. Use `rxMethod` wired in `withHooks.onInit`.

## Inject via default parameters

```typescript
// Correct
withMethods((store, dialog = inject(MatDialog)) => ({ ... }))

// Wrong
withMethods((store) => {
  const dialog = inject(MatDialog);
  return { ... };
})
```

