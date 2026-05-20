# Application architecture

Thin hub for **how this app is structured**. Detailed rules live in the linked standards—avoid duplicating them here.

## Layers (data flow)

Roughly:

1. **UI** — Components and templates: render state, fire events, thin handlers. See [angular-components.md](angular-components.md), [templates-and-styling.md](templates-and-styling.md).
2. **Orchestration** — **Stores** (NgRx Signal Store): coordinate flows, call services, own cross-cutting outcomes (e.g. snackbar, analytics) when that is the established pattern. See [state-and-stores.md](state-and-stores.md).
3. **I/O** — **Services**: Firebase, HTTP, auth helpers, domain APIs. Single responsibility; callers stay in stores for business flows. See [services-and-side-effects.md](services-and-side-effects.md).

**Rule of thumb:** Components do **not** call analytics, Firestore, or arbitrary HTTP for feature work—go through a store method that delegates ([services-and-side-effects.md](services-and-side-effects.md)).

**Local vs app-wide:** Feature-scoped `**signalStore`** (e.g. dialog flow) vs root `**providedIn: 'root'`** stores (shared app state) is spelled out in [state-and-stores.md](state-and-stores.md).

## Source layout (`src/app`)


| Area        | Role                                                                                                                            |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `core/`     | App-wide singletons: stores (e.g. `BuilderStore`), auth, analytics, shared services, models used across features.               |
| `features/` | Route-level areas (e.g. `builder/`, `landing/`, `admin/`): screens, feature components, colocated stores when feature-specific. |
| `shared/`   | Reusable UI and flows used from multiple features (e.g. auth dialog and its local store).                                       |


New work should **colocate** stores and types with the feature or shared folder that owns the behavior.

## Canonical examples

- **App store + services:** `src/app/core/store/builder.store.ts` (orchestration touching core services).
- **Local store + thin components:** `src/app/shared/components/auth-dialog/` — `AuthDialogStore` with sub-components; delegates to app-level store/services for real I/O.

## Angular “shape”

Standalone components, lazy-loaded feature routes, signals: [angular-components.md](angular-components.md) (section *Architecture* — Angular mechanics, not folder layout).

## See also


| Topic                                    | Doc                                                          |
| ---------------------------------------- | ------------------------------------------------------------ |
| Store patterns, `rxMethod`, inject style | [state-and-stores.md](state-and-stores.md)                   |
| Components vs stores vs services         | [services-and-side-effects.md](services-and-side-effects.md) |
| Splitting large UIs                      | [templates-and-styling.md](templates-and-styling.md)         |
| Forms                                    | [forms.md](forms.md)                                         |


