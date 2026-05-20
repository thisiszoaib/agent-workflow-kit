# Services and side effects

## Services

- Single responsibility—one domain per service.
- `providedIn: 'root'` for singletons.
- Use `inject()`, not constructor injection.
- Return `Promise` or `Observable` from data methods; let the caller compose.

## Components vs stores

**Components must not** call services directly for business side effects (analytics, Firestore, HTTP). They should call **store** methods that delegate to services.

**Components own:** local UI signals, local computeds for display, thin template handlers, `MatDialogRef` lifecycle.

**Audit:** Flag direct `analytics.event(...)`, Firestore, or HTTP calls from components; expose a store method instead.

### Thin handlers

Handlers should be 1–3 lines. If a handler has `try/catch`, loading flags, and a store call, consider moving loading and errors into the store (return a result the component uses).

See also: [state-and-stores.md](state-and-stores.md), [architecture.md](architecture.md) (folder layout and layers).