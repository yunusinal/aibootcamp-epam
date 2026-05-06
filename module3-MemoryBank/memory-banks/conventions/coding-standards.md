# Coding Standards: Personal Task Board

## Naming Conventions

### Files

| Type | Convention | Example |
|------|-----------|---------|
| React Components | PascalCase, `.tsx` extension | `TaskCard.tsx` |
| Custom Hooks | camelCase with `use` prefix, `.ts` extension | `useLocalStorage.ts` |
| Utility Functions | camelCase, `.ts` extension | `formatDate.ts` |
| Type Definitions | PascalCase, `.types.ts` suffix | `Board.types.ts` |
| CSS Modules | camelCase matching component, `.module.css` suffix | `taskCard.module.css` |
| Spec Files (PRD) | `prd-{slug}.md` | `prd-task-board.md` |
| Spec Files (Epic) | `epic-{NNN}-{slug}.md` (zero-padded 3 digits) | `epic-001-core-task-management.md` |
| Spec Files (Story) | `story-{NNN}.{N}-{slug}.md` | `story-001.1-create-task.md` |

### Code Identifiers

| Item | Convention | Example |
|------|-----------|---------|
| Variables & functions | camelCase | `taskCount`, `handleDelete()` |
| React components | PascalCase | `TaskCard`, `BoardSelector` |
| TypeScript interfaces | PascalCase, no `I` prefix | `Task`, `Board` |
| TypeScript type aliases | PascalCase | `ColumnType`, `DragPayload` |
| Constants | UPPER_SNAKE_CASE | `MAX_TASKS_PER_BOARD`, `STORAGE_KEY` |
| CSS class names (modules) | camelCase | `.taskCard`, `.columnHeader` |
| Event handlers | `handle` + Event | `handleClick`, `handleDragStart` |
| Boolean variables | `is`/`has`/`can` prefix | `isEditing`, `hasDescription`, `canDelete` |

---

## File Structure

```
src/
├── components/        # One folder per component
│   ├── TaskCard/
│   │   ├── TaskCard.tsx
│   │   └── taskCard.module.css
│   ├── Column/
│   │   ├── Column.tsx
│   │   └── column.module.css
│   └── BoardSelector/
│       ├── BoardSelector.tsx
│       └── boardSelector.module.css
├── hooks/             # Custom React hooks (shared logic)
│   ├── useLocalStorage.ts
│   ├── useDragAndDrop.ts
│   └── useKeyboardShortcuts.ts
├── types/             # Shared TypeScript types
│   ├── Board.types.ts
│   └── Task.types.ts
├── utils/             # Pure helper functions
│   └── sanitize.ts
├── App.tsx            # Root component
└── main.tsx           # Vite entry point
```

### Rules
- **One component per file** — do not export multiple components from a single file
- **Co-locate CSS** — each component's `.module.css` lives next to its `.tsx` file
- **Hooks folder** — only for hooks shared across multiple components; component-specific hooks stay in the component folder
- **Types folder** — only for types used by 2+ files; component-local types stay in the component file

---

## Code Organization

### Component Structure (top to bottom)
1. Imports (grouped: React → external libs → internal modules → relative imports → CSS)
2. Type definitions (if local to this component)
3. Component function declaration (`function TaskCard(props: TaskCardProps)`)
4. Hooks (useState, useEffect, custom hooks)
5. Derived state / computed values
6. Event handlers
7. Render (return JSX)
8. Export (default export at bottom)

### Function Guidelines
- **Maximum function length:** 50 lines (extract helpers if longer)
- **Single responsibility:** each function does one thing
- **Pure functions preferred** for utilities — no side effects
- **No class components** — functional components with hooks only

### React Patterns
- Use `useState` for simple local state
- Use `useReducer` for complex state with multiple sub-values
- Extract logic into custom hooks when shared across components
- Avoid prop drilling beyond 2 levels — restructure component tree instead
- Memoize expensive computations with `useMemo`; memoize callbacks with `useCallback` only when passed to optimized child components

---

## Comments

- **No unnecessary comments** — code should be self-explanatory via naming
- **JSDoc required** for exported utility functions and custom hooks:
  ```ts
  /** Reads and parses a value from localStorage. Returns fallback if key is missing or invalid. */
  function useLocalStorage<T>(key: string, fallback: T): [T, (value: T) => void] { ... }
  ```
- **TODO format:** `// TODO: Description of what needs to be done`
- **Do not comment out dead code** — delete it (Git tracks history)

---

## TypeScript Rules

- **Strict mode enabled** — `"strict": true` in `tsconfig.json`
- **No `any` type** — use `unknown` and narrow, or define proper types. If `any` is truly unavoidable, add a `// eslint-disable-next-line` comment explaining why
- **Prefer interfaces** for object shapes, **type aliases** for unions/intersections
- **Explicit return types** on exported functions and hooks
- **No type assertions** (`as`) unless interfacing with DOM APIs (e.g., `e.target as HTMLInputElement`)

---

## Testing Requirements

### Test Types
| Type | Tool | When to Write |
|------|------|---------------|
| Unit tests | Vitest | Utility functions, custom hooks, pure logic |
| Component tests | React Testing Library + Vitest | User interactions, rendering, state changes |
| Accessibility audits | axe-core | After each component is complete |

### Coverage Targets
- **Utility functions:** 100% branch coverage
- **Custom hooks:** 100% for public API
- **Components:** cover all acceptance criteria from the story
- **Overall minimum:** 80% line coverage

### Test File Conventions
- Test file lives next to source file: `TaskCard.test.tsx` alongside `TaskCard.tsx`
- Use `describe` blocks grouped by feature/behavior
- Use `it` (not `test`) for individual test cases
- Test names read as sentences: `it('displays task title in the card')`
- Prefer `screen.getByRole` and `screen.getByLabelText` over `getByTestId`

---

## Error Handling

### User-Facing Errors
- Display clear, actionable messages (e.g., "Storage is full. Delete some tasks to continue.")
- Never show raw error objects, stack traces, or technical jargon to users
- Use a consistent error display pattern (inline message near the action that failed)

### localStorage Errors
- Wrap `localStorage.setItem` in try/catch to handle `QuotaExceededError`
- On read failure (corrupted JSON), fall back to default empty state and log a warning to console
- Never silently swallow errors — at minimum log to `console.warn`

### Validation
- Validate at system boundaries: form inputs, localStorage reads, drag-and-drop payloads
- Task title is required and must be non-empty after trimming
- Do not over-validate internal function calls between trusted components

---

## Security

- **XSS prevention:** all user-provided text (task titles, descriptions) is rendered via React JSX (auto-escaped). Never use `dangerouslySetInnerHTML`
- **Input sanitization:** trim whitespace from task titles before saving
- **No external requests:** the app must make zero network calls — no analytics, no CDN fonts at runtime, no third-party scripts

---

## Accessibility (WCAG 2.1 Level AA)

- All interactive elements reachable via keyboard `Tab` navigation
- Visible focus indicators on all focusable elements (minimum 2px outline)
- Color contrast ratio ≥ 4.5:1 for normal text, ≥ 3:1 for large text
- Drag-and-drop has keyboard-accessible alternative (arrow keys / shortcut keys)
- ARIA labels on icon-only buttons (e.g., delete button)
- Live region announcements (`aria-live="polite"`) for dynamic content changes (task moved, task deleted)
- Semantic HTML: use `<button>` for actions, `<input>` for text entry, `<h2>` for column headers

---

## Quality Criteria (Definition of Done)

Before any story implementation is considered complete:

- [ ] All acceptance criteria from the story pass
- [ ] No TypeScript errors (`tsc --noEmit` passes)
- [ ] No ESLint warnings or errors
- [ ] No `any` types introduced
- [ ] Component follows single-responsibility principle
- [ ] User-facing text sanitized (no `dangerouslySetInnerHTML`)
- [ ] localStorage persistence verified (write → close → reopen → data intact)
- [ ] Keyboard accessibility works for all new interactive elements
- [ ] No features added beyond the story's scope
- [ ] CSS follows module conventions (no global styles leaked)