# AGENTS.md — Specification-Driven Development (SDD)

This project follows **Specification-Driven Development (SDD)**, where all implementation is guided by a strict hierarchy of specifications. AI agents must always work within this hierarchy and never implement features without a corresponding spec.

---

## Specification Hierarchy

```
PRD → Epic(s) → Story(ies) → Implementation
```

| Level | Purpose | Location | Template |
|-------|---------|----------|----------|
| PRD | Product vision, personas, requirements | `specs/prds/` | `specs/templates/prd-template.md` |
| Epic | Large feature grouping (3–4 per PRD) | `specs/epics/` | `specs/templates/epic-template.md` |
| Story | Single deliverable unit (5–7 per Epic) | `specs/stories/` | `specs/templates/story-template.md` |

**Rule:** Never skip a level. Implementation requires a Story. Stories require a parent Epic. Epics require a parent PRD.

---

## Tech Stack

- **Frontend:** React 18 + Vite
- **Language:** TypeScript (strict mode)
- **Styling:** CSS Modules (or plain CSS — no external UI libraries)
- **State/Storage:** localStorage — no backend, no database
- **Package Manager:** npm
- **Build Target:** Modern browsers (ES2020+)

---

## Agent Roles

### 1. Product Analyst Agent

**Trigger:** User provides a project brief or asks to create/update a PRD.

**Responsibilities:**
- Generate PRDs from project briefs using `specs/templates/prd-template.md`
- Ensure problem statements include quantified pain points
- Define SMART success metrics with baselines and targets
- Create named personas with concrete goals and frustrations
- Write testable functional requirements using "shall" statements

**Prompt file:** `.github/prompts/generate-prd.prompt.md`

**Output:** `specs/prds/prd-{slug}.md`

---

### 2. Epic Decomposition Agent

**Trigger:** User asks to break down a PRD into epics.

**Responsibilities:**
- Read a PRD and identify 3–4 epics that cover all functional requirements
- Ensure each epic delivers end-to-end user value (no "backend-only" epics)
- Map each epic to at least one PRD success metric
- Minimize cross-epic dependencies
- Size epics at S or M (split if L)

**Prompt file:** `.github/prompts/decompose-epics.prompt.md`

**Output:** `specs/epics/epic-{NNN}-{slug}.md`

---

### 3. Story Decomposition Agent

**Trigger:** User asks to break an epic into user stories.

**Responsibilities:**
- Read an epic and produce 5–7 user stories following INVEST principles
- Use "As a [named persona], I want [action] so that [benefit]" format
- Write 3–5 acceptance criteria per story in Given/When/Then format
- Estimate using Fibonacci points (1, 2, 3, 5 — never 8+)
- Ensure stories are completable in 1–3 days by a single developer

**Decomposition strategy:**
1. Foundation story — minimal core action (create/read)
2. Enhancement stories — additional CRUD (update, delete)
3. Validation / error handling — edge cases, error states
4. UX polish — feedback, animations, empty states
5. Integration stories — persistence, connecting features

**Prompt file:** `.github/prompts/decompose-stories.prompt.md`

**Output:** `specs/stories/story-{epic-number}.{story-number}-{slug}.md`

---

### 4. Implementation Agent

**Trigger:** User asks to implement a specific story.

**Responsibilities:**
- Read the target story's acceptance criteria before writing any code
- Implement ONLY what the story requires — no scope creep
- Follow project conventions (tech stack, naming, structure)
- Validate all acceptance criteria are met
- Do not introduce features from other stories

**Before implementing, always:**
1. Read the story file completely
2. Read the parent epic for context
3. Check if dependent stories exist and their status
4. Confirm scope with user if requirements are ambiguous

**Constraints:**
- No `any` types unless unavoidable (document why)
- One responsibility per component; extract hooks for logic
- All user text sanitized before rendering (XSS prevention)
- localStorage persistence verified (write → reload → read)
- Keyboard accessibility for all interactive elements

---

### 5. Review / QA Agent

**Trigger:** User asks to review implementation against specs.

**Responsibilities:**
- Verify each acceptance criterion from the story is satisfied
- Check that no extra scope was added beyond the story
- Validate naming conventions and file organization
- Ensure accessibility requirements (WCAG 2.1 AA) are met
- Confirm localStorage persistence works correctly
- Run through edge cases listed in acceptance criteria

---

## SDD Workflow Sequence

```
1. User provides project brief
       ↓
2. Product Analyst Agent → generates PRD
       ↓
3. Epic Decomposition Agent → breaks PRD into 3–4 epics
       ↓
4. Story Decomposition Agent → breaks each epic into 5–7 stories
       ↓
5. Implementation Agent → implements one story at a time
       ↓
6. Review Agent → validates implementation against story criteria
       ↓
7. Repeat steps 5–6 for remaining stories
```

---

## Workflow Rules

### General Rules (All Agents)

1. **Always read the relevant spec before acting.** Never assume — verify against the spec file.
2. **Use templates for new specs.** All new PRDs, epics, and stories must be based on `specs/templates/`.
3. **Maintain traceability.** Every story references its epic; every epic references its PRD.
4. **IDs must be unique.** Check existing files before assigning new numeric IDs.
5. **No placeholders in output.** Every section must contain specific, actionable content.
6. **Naming conventions are mandatory.** Lowercase hyphen-separated slugs, zero-padded 3-digit IDs, ≤ 4 words.
7. **No backend.** All persistence uses `localStorage`. Do not introduce APIs or databases.

### Implementation Boundaries

- **One story at a time.** Never implement multiple stories without explicit user approval.
- **No forward references.** Do not implement features belonging to unwritten stories.
- **Respect "Out of Scope."** If a PRD/epic explicitly excludes something, do not build it.
- **Dependencies are documented.** If Story B depends on Story A, confirm A is complete first.

---

## Naming Conventions

### Spec Files

| Type | Pattern | Example |
|------|---------|---------|
| PRD | `specs/prds/prd-{slug}.md` | `prd-task-board.md` |
| Epic | `specs/epics/epic-{NNN}-{slug}.md` | `epic-001-core-task-management.md` |
| Story | `specs/stories/story-{NNN}.{N}-{slug}.md` | `story-001.1-create-task.md` |

### Source Code

| Item | Convention | Example |
|------|-----------|---------|
| Components | PascalCase | `TaskCard.tsx` |
| Hooks | camelCase, `use` prefix | `useLocalStorage.ts` |
| Utilities | camelCase | `formatDate.ts` |
| Types/Interfaces | PascalCase, `.types.ts` suffix | `Board.types.ts` |
| CSS Modules | camelCase classes | `taskCard.module.css` |

---

## File Organization

```
task-board-lab/
├── agents.md              # This file — SDD agent instructions
├── .github/prompts/       # Reusable prompt files for each agent role
├── specs/                 # Specifications (PRDs, epics, stories, templates)
├── public/                # Static assets
├── src/
│   ├── components/        # React components (one folder per component)
│   ├── hooks/             # Custom React hooks
│   ├── types/             # Shared TypeScript types
│   ├── utils/             # Helper functions
│   ├── App.tsx            # Root component
│   └── main.tsx           # Vite entry point
├── index.html             # Vite HTML entry
├── tsconfig.json
├── vite.config.ts
└── package.json
```

---

## Project Constraints

| Constraint | Details |
|-----------|---------|
| Frontend only | React 18 + Vite, no backend |
| Language | TypeScript strict mode, no `any` |
| Styling | CSS Modules or plain CSS — no Tailwind, no MUI |
| State | localStorage — no Redux, no external state libraries |
| Package manager | npm |
| Browser targets | ES2020+, last 2 versions of Chrome/Firefox/Safari/Edge |
| Accessibility | WCAG 2.1 Level AA compliance |
| Performance | Initial render ≤ 500ms with 50 tasks |
| Data limits | ≤ 100 tasks per board, ≤ 10 boards, ≤ 5MB localStorage |

---

## Quality Gates

### Before a spec is "Done":

- [ ] All template sections filled — no `[TBD]` or `[FILL IN]` remains
- [ ] Parent reference is correct (story → epic → PRD)
- [ ] ID is unique across all files in that category
- [ ] Naming convention followed exactly
- [ ] Content is specific and measurable (no vague adjectives)

### Before implementation is "Done":

- [ ] All acceptance criteria from the story pass
- [ ] Code reviewed — no lint or TypeScript errors
- [ ] No new `any` types introduced
- [ ] Component follows single-responsibility principle
- [ ] User-facing text sanitized (XSS prevention)
- [ ] localStorage persistence verified (write → reload → read)
- [ ] Keyboard accessibility works for all interactive elements
- [ ] No features added beyond story scope
