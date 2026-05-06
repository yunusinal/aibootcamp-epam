# Development Workflow: Personal Task Board

## Development Process

### From Idea to Production (SDD Workflow)

This project follows **Spec-Driven Development (SDD)**. Every feature flows through the full specification hierarchy before any code is written.

```
1. Project Brief (plain-language idea)
       ↓
2. PRD (Product Analyst Agent generates PRD)
       ↓
3. Epics (Epic Decomposition Agent breaks PRD into 3–4 epics)
       ↓
4. Stories (Story Decomposition Agent breaks each epic into 5–7 stories)
       ↓
5. Implementation (Implementation Agent builds one story at a time)
       ↓
6. Review (Review/QA Agent validates against story acceptance criteria)
       ↓
7. Repeat steps 5–6 for remaining stories
```

### Key Rule: Never Skip a Level
- You cannot implement code without a Story
- You cannot write a Story without a parent Epic
- You cannot create an Epic without a parent PRD
- Traceability must be maintained at every level

---

## Story Implementation Workflow (Day-to-Day)

When implementing a single story, follow this sequence:

### 1. Read the Story (5 min)
- Open the story file from `specs/stories/`
- Read every acceptance criterion carefully
- Identify any ambiguity — resolve before coding

### 2. Read the Parent Epic (2 min)
- Open the parent epic from `specs/epics/`
- Understand how this story fits into the larger feature
- Check if any dependent stories need to be completed first

### 3. Plan the Implementation (5 min)
- Identify which files need to be created or modified
- Determine the component structure and data flow
- Decide on types/interfaces needed

### 4. Write Types First (5 min)
- Define TypeScript interfaces and types in `src/types/`
- Ensure types align with the story's data requirements

### 5. Implement the Feature (20–60 min)
- Build components, hooks, and utilities
- Follow conventions from `memory-banks/conventions/coding-standards.md`
- Implement ONLY what the story requires — no scope creep

### 6. Write Tests (15–30 min)
- Write unit tests for utility functions and hooks
- Write component tests for user interactions
- Verify all acceptance criteria are covered by tests

### 7. Self-Review (10 min)
- Run `tsc --noEmit` — zero TypeScript errors
- Run `npm run lint` — zero ESLint warnings
- Run `npm test` — all tests pass
- Check the Quality Gates checklist (see below)

### 8. Verify Persistence (5 min)
- Create/modify data in the app
- Close the browser tab
- Reopen — verify data is intact from localStorage

---

## Branching Strategy

### Pattern: GitHub Flow (Simplified)

Since this is a solo developer project, we use a simplified branching model:

| Branch | Purpose | Rules |
|--------|---------|-------|
| `main` | Stable, deployable code | Always passes all tests; never commit directly |
| `feature/{story-slug}` | Story implementation | One branch per story; merge via PR |
| `fix/{description}` | Bug fixes | For issues found after story completion |

### Branch Naming Convention
- Feature: `feature/story-001.1-create-task`
- Bug fix: `fix/localstorage-parse-error`
- Use lowercase, hyphens, and the story ID when applicable

### Workflow
1. Create branch from `main`: `git checkout -b feature/story-001.1-create-task`
2. Implement the story (multiple commits are fine)
3. Push and create a Pull Request
4. Self-review against the checklist below
5. Merge to `main` after all checks pass
6. Delete the feature branch

---

## Pull Request Process

### Before Creating a PR
- [ ] All acceptance criteria from the story pass
- [ ] `tsc --noEmit` passes (zero TypeScript errors)
- [ ] `npm run lint` passes (zero ESLint warnings)
- [ ] `npm test` passes (all tests green)
- [ ] No `any` types introduced
- [ ] localStorage persistence verified manually

### PR Description Template
```markdown
## Story
Link: `specs/stories/story-{NNN}.{N}-{slug}.md`

## What Changed
- [Brief list of files added/modified]

## Acceptance Criteria Verification
- [ ] AC1: [paste criterion] — PASS
- [ ] AC2: [paste criterion] — PASS
- [ ] AC3: [paste criterion] — PASS

## Screenshots (if UI changes)
[Attach screenshots showing the feature]
```

### Code Review Checklist
- [ ] Follows naming conventions (PascalCase components, camelCase hooks/utils)
- [ ] One component per file
- [ ] No `dangerouslySetInnerHTML` usage
- [ ] All interactive elements keyboard-accessible
- [ ] No features beyond the story's scope
- [ ] CSS uses modules (no global style leaks)
- [ ] Error cases handled (localStorage full, invalid JSON)

---

## Testing Strategy

### Test Pyramid

```
       ╱╲
      ╱  ╲       Manual/Visual (accessibility spot checks)
     ╱────╲
    ╱      ╲     Component Tests (React Testing Library)
   ╱────────╲
  ╱          ╲   Unit Tests (Vitest — hooks, utils, pure logic)
 ╱────────────╲
```

### What to Test at Each Level

**Unit Tests (Vitest)**
- Utility functions (e.g., sanitize, ID generation, JSON parsing)
- Custom hooks (e.g., useLocalStorage read/write behavior)
- Pure logic (e.g., moving a task between columns, reordering)

**Component Tests (React Testing Library)**
- User interactions (click to create task, type title, submit)
- Rendering (task card displays title, column shows correct count)
- State transitions (task moves from To Do to In Progress)
- Keyboard shortcuts trigger correct actions
- Accessibility (elements have correct ARIA attributes)

**Manual/Visual Checks**
- Drag-and-drop feels responsive (< 100ms visual feedback)
- Layout looks correct at 768px and 1920px viewports
- Focus indicators are visible during keyboard navigation
- Color contrast meets WCAG 4.5:1 ratio

### Coverage Requirements
- **Minimum overall:** 80% line coverage
- **Utilities and hooks:** 100% branch coverage
- **Critical paths:** localStorage persistence, task CRUD operations

### Test File Naming
- Component: `TaskCard.test.tsx` (next to `TaskCard.tsx`)
- Hook: `useLocalStorage.test.ts` (next to `useLocalStorage.ts`)
- Utility: `sanitize.test.ts` (next to `sanitize.ts`)

---

## Build & Deployment Process

### Local Development
```bash
npm install          # Install dependencies (first time)
npm run dev          # Start Vite dev server on localhost:5173
```

### Production Build
```bash
npm run build        # Output optimized static files to dist/
npm run preview      # Preview production build locally
```

### Deployment
1. Run `npm run build` to generate `dist/` folder
2. Deploy `dist/` contents to any static file host:
   - GitHub Pages
   - Netlify (drag-and-drop deploy)
   - Vercel
   - Any simple HTTP server
3. No environment variables needed — no backend, no API keys

### CI/CD Pipeline (GitHub Actions)
```
Push to any branch
  → npm ci (install deps)
  → npm run lint (ESLint)
  → tsc --noEmit (type check)
  → npm test (Vitest)
  → npm run build (production build)

Merge to main
  → All above steps +
  → Deploy dist/ to static host
```

### Rollback
- Revert the merge commit on `main` and re-deploy
- Static files make rollback trivial — no database migrations, no server state

---

## Verification After Deployment

### Smoke Test Checklist
- [ ] App loads without errors in browser console
- [ ] Can create a new task
- [ ] Can move a task between columns (drag-and-drop)
- [ ] Can move a task via keyboard shortcut (`M`)
- [ ] Can delete a task with confirmation
- [ ] Reload page — all data persists
- [ ] Switch boards — data is independent
- [ ] Keyboard shortcuts work (`N`, `J`, `K`, `M`, `D`, `?`)

---

## Troubleshooting Common Issues

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Data lost after reload | localStorage key mismatch or write failure | Check `useLocalStorage` hook; verify `setItem` is called on every state change |
| TypeScript errors on build | Strict mode catching issues | Run `tsc --noEmit` locally; fix all type errors before pushing |
| Drag-and-drop not working | Missing event handlers or incorrect state update | Verify `onDragStart`, `onDragOver`, `onDrop` are wired correctly |
| Keyboard shortcuts fire while typing | Missing check for active input focus | Guard shortcuts with `document.activeElement.tagName !== 'INPUT'` |
| Styles leaking between components | Using global CSS instead of CSS Modules | Ensure all class names come from `.module.css` imports |