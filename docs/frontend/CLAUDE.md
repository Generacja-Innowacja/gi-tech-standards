# CLAUDE.md — Generacja Innowacja Front-End Standards

> **Purpose of this file:** condensed, machine-readable reference of all front-end standards from
> `docs/frontend/`. Use it as context when generating developer tasks, scoping tickets, reviewing PRs,
> writing acceptance criteria, or scaffolding new projects. Every rule below is enforceable — if a
> task contradicts it, the task description must call out the deviation explicitly and reference an
> approval from the Technical Leader.

---

## 0. Meta rules for task generation

When generating developer tasks based on this document:

- Always reference the canonical doc path (e.g. `docs/frontend/conventions/NAMING.md`) in the ticket
  description so the dev can drill in.
- Acceptance criteria must be testable against the conventions in §3 and tooling in §4.
- New projects must be bootstrapped from the
  [Vite Project Boilerplate](https://github.com/Generacja-Innowacja/vite-project-boilerplate). If a
  task creates a new repo, add a sub-task: "scaffold from vite-project-boilerplate".
- Any deviation from §4 (tooling) requires a sub-task: "obtain Technical Leader approval for
  <tech>".
- Default Definition of Done for any front-end task includes: lints clean (Biome), types clean
  (TypeScript strict), unit tests added/updated, e2e covers happy path if user-facing flow changed.

---

## 1. Stack at a glance

| Layer | Tool | Min version | Notes |
|---|---|---|---|
| Runtime | Node.js | >= 24 | Latest LTS only. |
| Package manager | Yarn | >= 1.22 | Lockfile must be committed. No npm/pnpm mixing. |
| Language | TypeScript | >= 5.9 | Strict mode assumed. |
| UI lib | React | >= 19 | |
| Build tool | Vite | >= 7 | |
| Routing | React Router | >= 7.9 | **Framework Mode** — not the legacy data router setup. |
| Styling | Tailwind CSS | >= 4 | Utility-first; avoid custom CSS unless unavoidable. |
| State (default) | React Context + `useState` | — | First reach. |
| State (complex) | Zustand | — | When Context is the wrong tool (perf, persistence, middleware). |
| HTTP | Axios | — | Use interceptors for auth/error handling. |
| Schema validation | Zod | — | Validate every API response; derive TS types from schemas. |
| Linter + formatter | Biome | — | Replaces ESLint + Prettier. Base ruleset + Unicorn overrides. |
| Unit tests | Vitest + React Testing Library + React Test Renderer | — | Target coverage **95–100%**. |
| E2E tests | Playwright + Gherkin | — | All happy paths. |
| Component docs | Storybook | — | Living style guide for shared/design-system components. |

When you write a task that introduces a library, **default to "use the existing tool"**. Suggest a
new dependency only when nothing in the table above can do the job, and flag it as needing TL
approval.

---

## 2. Project structure (the only allowed layout)

```txt
|- public/                          # Non-functional static assets (favicon, thumbnails, etc.)
|- e2e/
|   |- [domain-name]/               # E2E grouped by domain
|       |- path-name.spec.ts        # Playwright spec, BDD/Gherkin style
|- src/
|   |- pages/                       # Route-level page components
|   |- components/
|   |   |- shared/                  # Cross-domain reusable components
|   |   |   |- [ComponentName]/
|   |   |- [domain-name]/           # Domain-specific components (home, admin, quiz, ...)
|   |       |- [ComponentName]/
|   |- services/                    # API clients — encapsulated per backend
|   |   |- [api-name]/              # e.g. api/, cms/
|   |       |- schemas/             # Zod schemas / data models
|   |       |- client/              # Axios instance + config
|   |       |- utils/               # Client helpers (interceptors, transforms)
|   |- constants/
|   |   |- [domain-name].ts         # e.g. common.ts, user.ts, config.ts
|   |- types/
|   |   |- [domain-name].ts         # Global types, split by domain
|   |- utils/
|   |   |- [domain-name]/           # e.g. number/, text/, object/
|   |       |- transformNumber.ts
|   |       |- transformNumber.test.ts
|   |- assets/
|       |- icons/                   # SVGs
|       |- images/                  # JPG, PNG, WebP, ...
```

Hard rules:

- **Domain code stays separated from global code.** Domain-only components live under
  `src/components/[domain-name]/`; only promote to `shared/` when ≥2 domains use it.
- **Every API client is encapsulated** under `src/services/[api-name]/`. Pages/components must not
  instantiate Axios or call `axios.get` directly.
- **All reusable code is easy to find.** If a util/type/constant is used in more than one domain, it
  belongs in `src/utils/`, `src/types/`, or `src/constants/` — not next to a single component.

When a ticket spans multiple files, follow the structure above when adding new files. Do not invent
new top-level folders without TL approval.

---

## 3. Conventions

### 3.1 Naming (`docs/frontend/conventions/NAMING.md`)

- Functions / variables → `camelCase`
- React components → `PascalCase`
- Everything else → `kebab-case`

Concrete:

| Entity | Pattern | Example |
|---|---|---|
| Domain folder | `kebab-case` | `user-profile/` |
| Component folder | `PascalCase` | `UserProfileCard/` |
| Other folders | `kebab-case` | `utils/`, `schemas/` |
| Component file | `PascalCase.<type>.<ext>` | `UserProfileCard.tsx`, `UserProfileCard.types.ts` |
| Asset | `kebab-case.ext` | `arrow-right.svg`, `hero-banner.jpg` |
| Util / hook | `camelCase.ext` | `formatCurrency.ts`, `useDebounce.ts` |

Tasks that create files must use these patterns in acceptance criteria.

### 3.2 Component structure (`docs/frontend/conventions/COMPONENT_STRUCTURE.md`)

Three principles:

1. **Encapsulation** — types, utils, constants, and subcomponents used by only one component live
   inside that component's folder. If they're shared, they get promoted to globals.
2. **Minimization** — only create files/folders that are actually needed. No empty `index.ts`,
   `types.ts` etc. just for show.
3. **Mirroring** — folder structure mirrors the component tree (parent → subcomponent folders
   nested).

Canonical layout for a component:

```txt
|- ComponentName/
    |- ComponentName.tsx              # View
    |- ComponentName.test.ts          # Unit tests
    |- ComponentName.types.ts         # Component-scoped types
    |- ComponentName.constants.ts     # Component-scoped constants
    |- utils/                         # Component-scoped utils/hooks (only if needed)
    |   |- getSomeData.ts
    |   |- getSomeData.test.ts
    |- SubComponent/                  # Nested subcomponent (recursive structure)
    |- OtherSubComponent/
```

When writing a "create component X" task, default to listing the files above and explicitly drop the
ones not needed (rather than the other way around).

### 3.3 Testing convention (`docs/frontend/conventions/TESTING_CONVENTION.md`)

Use **BDD / Given–When–Then** structure for both unit and e2e tests.

Vitest pattern:

```ts
describe('<Button />', () => {       // Given
  describe('when clicked', () => {   // When
    it('calls the handler', () => {  // Then
      const handleClick = vi.fn();
      render(<Button onClick={handleClick}>Click me</Button>);
      fireEvent.click(screen.getByText('Click me'));
      expect(handleClick).toHaveBeenCalledTimes(1);
    });
  });
});
```

Playwright/Gherkin pattern:

```gherkin
Given a user is on the login page
When they enter valid credentials
Then they should be redirected to the dashboard
```

Acceptance-criteria phrasing for testing tasks should mirror Given/When/Then so devs translate
1:1 into test cases.

---

## 4. Tooling rules (per file in `docs/frontend/tools/`)

### 4.1 Fundamentals

- Node 24+, Yarn 1.22+, TypeScript 5.9+ — see §1.
- New projects must declare engines in `package.json` matching these versions.

### 4.2 React stack

- React 19+, Vite 7+, Tailwind 4+, React Router 7.9+ in **Framework Mode**.
- Storybook for any component intended for `shared/` or design-system reuse — a shared component
  without a story is incomplete.

### 4.3 State management

- Default: `useState` + `useContext`. Use this for theme, user prefs, simple shared state.
- Escalate to **Zustand** only when one of these triggers fires:
  - Frequent updates causing Context re-render perf issues.
  - State must persist across sessions (localStorage etc.).
  - Need for middleware (logging, devtools, persistence).
  - Multi-action complex global state.
- Tickets that introduce Zustand should justify which trigger applies.

### 4.4 API communication

- HTTP client: **Axios** with interceptors for auth + error normalization.
- Validation: **Zod** schemas validate every API response at runtime; derive TS types via
  `z.infer<typeof schema>`.
- Schemas live in `src/services/[api-name]/schemas/`. Client config in `client/`. Helpers in
  `utils/`.

### 4.5 Code quality

- **Biome** (Rust-based) replaces ESLint + Prettier. Base ruleset + **Unicorn** overrides.
- Lint runs on every commit and in CI.
- CI pipeline jobs (build, lint, test, e2e) must all pass before merge.

### 4.6 Testing

- **Pyramid:** lots of unit tests, few e2e tests.
- Unit: Vitest + @testing-library/react + React Test Renderer; **target 95–100% coverage**.
- E2E: Playwright + Gherkin; cover **all happy paths** (edge cases belong in unit tests).

---

## 5. Definition of Done — copy/paste into tickets

```md
- [ ] Code follows folder structure (docs/frontend/conventions/PROJECT_STRUCTURE.md)
- [ ] Naming follows docs/frontend/conventions/NAMING.md
- [ ] Component layout follows docs/frontend/conventions/COMPONENT_STRUCTURE.md
- [ ] Unit tests added/updated, BDD style, coverage ≥95% on changed files
- [ ] If user-facing: Playwright happy-path e2e added/updated (Gherkin)
- [ ] Biome lint clean (no disabled rules without justification)
- [ ] TypeScript clean (no `any`, no `@ts-ignore` without comment)
- [ ] API responses validated with Zod
- [ ] Storybook story added
- [ ] State escalation to Zustand justified in PR description (if applicable)
- [ ] CI green: build, lint, test, e2e
```

---

## 6. Quick decision tree (for ticket triage)

- "Where does this component go?" → used by ≥2 domains? `components/shared/`. Otherwise
  `components/[domain]/`.
- "Should I add Zustand?" → can Context + useState do it without perf pain or middleware? If yes,
  no.
- "Should I write a custom CSS file?" → almost never. Use Tailwind utilities. Justify the exception.
- "Should I use fetch?" → no. Use the Axios client from `services/[api-name]/client/`.
- "Should I trust the API response shape?" → no. Run it through a Zod schema.
- "Where do unit tests live?" → next to the file under test, same name with `.test.ts(x)`.
- "Where do e2e tests live?" → `e2e/[domain]/[path-name].spec.ts`.
- "New top-level dependency or framework?" → needs Technical Leader approval; add a sub-task.

---

## 7. Source-of-truth doc map

| Topic | Doc |
|---|---|
| Index | `docs/frontend/INDEX.md` |
| Component structure | `docs/frontend/conventions/COMPONENT_STRUCTURE.md` |
| Naming | `docs/frontend/conventions/NAMING.md` |
| Project structure | `docs/frontend/conventions/PROJECT_STRUCTURE.md` |
| Testing convention (BDD) | `docs/frontend/conventions/TESTING_CONVENTION.md` |
| API communication | `docs/frontend/tools/API_COMMUNICATION.md` |
| Code quality | `docs/frontend/tools/CODE_QUALITY.md` |
| Fundamentals (Node/Yarn/TS) | `docs/frontend/tools/FUNDAMENTALS.md` |
| React stack | `docs/frontend/tools/REACT.md` |
| State management | `docs/frontend/tools/STATE_MANAGEMENT.md` |
| Testing tools | `docs/frontend/tools/TESTING.md` |
| Boilerplate | <https://github.com/Generacja-Innowacja/vite-project-boilerplate> |
