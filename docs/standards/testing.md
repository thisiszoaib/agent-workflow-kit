# Testing

## Unit tests (Material)

- Prefer **Material harnesses** (`MatButtonHarness`, `MatExpansionPanelHarness`, `MatSelectHarness`, `MatSliderHarness`, etc.) over raw `querySelector` / native `getByRole` on Material internals.
- Use `TestbedHarnessEnvironment.loader(fixture)` → `loader.getHarness(SomeHarness.with({ ... }))`.

**Reference:** [`.agents/skills/angular-developer/references/component-harnesses.md`](../../.agents/skills/angular-developer/references/component-harnesses.md) and `testing-fundamentals.md`.

## E2E (Playwright)

- Prefer semantic locators (`getByRole`, `getByLabel`) over CSS or component tag selectors for Material.
- Examples: `getByRole('combobox')` for `mat-select`, `getByRole('slider')` for `mat-slider`, `getByRole('switch')` for `mat-slide-toggle`, `getByRole('button', { name: /…/ })` for expansion panel headers, `getByRole('dialog')` for `mat-dialog`.

## Store / dialog mocks

- Mock `MatDialog.open` to return `{ afterClosed: () => of(undefined) }` when the store subscribes to `afterClosed`.
- Use `vi.fn()` (Vitest) for mocks.
- After `patchState` or async work, call `fixture.detectChanges()` or `TestBed.flushEffects()` as needed.
