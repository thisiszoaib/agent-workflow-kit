# Forms

## Signal Forms (required for new work)

- Use **Angular Signal Forms** (`@angular/forms/signals`: `form()`, `[formField]`, `FormField`, `submit()`, schema validators) for **every** new form.
- Do **not** add new `FormGroup` / `FormControl` / `FormBuilder` or template-driven (`ngModel`) forms unless migrating legacy code.

**Reference:** [`.agents/skills/angular-developer/references/signal-forms.md`](../../.agents/skills/angular-developer/references/signal-forms.md) and the main `SKILL.md` for patterns, validation, and Material inputs (`[formField]` on the control with `matInput`).

## Project rules

- Do **not** put the HTML `required` attribute on the same element as `[formField]`. Use `required()` in the schema; use `aria-required` for accessibility when needed.

## Submit behavior

- Per the [signal form submission guide](https://angular.dev/guide/forms/signals/form-submission), **`FormRoot`** sets `novalidate`, prevents default full-page submit, and wires submission when `form()` includes `submission` (when your package exports `FormRoot`).
- Until then, use `(submit)` on `<form>` and call `event.preventDefault()` in the handler. See [signal forms essentials](https://angular.dev/essentials/signal-forms).
- Do **not** rely on `FormsModule` / `NgForm` unless using template-driven or legacy reactive forms.

## Large UIs

When splitting templates by flow, keep `form()` / `FormGroup` / field models in the sub-component that owns that form unless there is a strong reason to lift them. The store can still own cross-flow prefill, loading flags, and method calls.
