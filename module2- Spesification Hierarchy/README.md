# Module 2: Specification Hierarchy

## What This Is

A hands-on exercise in **Spec-Driven Development (SDD)** — building a complete specification hierarchy for a Personal Task Board application, from project brief down to implementable stories.

## What I Learned

- **Specification Hierarchy:** PRD → Epics → Stories — never skip a level
- **PRD Writing:** Problem statements need quantified pain points, not vague complaints
- **Epic Decomposition:** Group by user workflow, not by technical layer
- **Story Writing:** INVEST principles, Given/When/Then acceptance criteria, Fibonacci estimation
- **ADRs:** Document *why* a technical decision was made, not just *what*
- **Agents.md:** A configuration file that tells AI assistants how to implement your specs consistently
- **Prompt Files:** Reusable `.prompt.md` files that act as agent instructions for each SDD role

## What I Built

```
specs/
├── project-brief.md              # Starting point — the "napkin idea"
├── prds/
│   └── prd-task-board.md         # Full PRD with personas, requirements, metrics
├── epics/
│   ├── epic-001-core-task-management.md
│   ├── epic-002-drag-and-drop.md
│   ├── epic-003-keyboard-shortcuts.md
│   └── epic-004-multi-board.md
├── stories/
│   ├── story-001.1 → 001.6      # Core task CRUD + persistence
│   ├── story-002.1 → 002.5      # Drag-and-drop interactions
│   ├── story-003.1 → 003.6      # Keyboard shortcuts
│   └── story-004.1 → 004.5      # Multi-board support
└── templates/                    # Reusable templates for PRD, Epic, Story
```

## Tools & Techniques Used

| Tool / Concept | Purpose |
|----------------|---------|
| **Copilot + Prompt Files** | AI-assisted spec generation via `.github/prompts/` |
| **Agents.md** | Defined agent roles, workflow rules, and quality gates |
| **PRD Template** | Structured format ensuring no section is skipped |
| **INVEST Criteria** | Quality checklist for well-formed user stories |
| **SMART Metrics** | Measurable success criteria with baselines and targets |
| **Given/When/Then** | Testable acceptance criteria format |

## Tech Stack (for the app being specified)

- React 18 + Vite + TypeScript (strict mode)
- CSS Modules — no UI libraries
- localStorage — no backend
- WCAG 2.1 AA accessibility

## Key Takeaway

> Write specs before code. If a requirement isn't testable, it isn't a requirement.