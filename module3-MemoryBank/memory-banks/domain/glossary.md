# Domain Glossary: Personal Task Board

## Core Concepts

### Board
**Definition:** A named container that holds a set of tasks organized into columns. Each board represents one project or work context.

**Context:** Users (especially Alex, the freelancer) manage 2–3 concurrent projects. Each project gets its own board so tasks stay separated. Switching between boards is instant.

**Constraints:** Maximum 10 boards per application. Each board has exactly three fixed columns (To Do, In Progress, Done). Board names must be non-empty.

**localStorage key pattern:** All boards are stored under a single JSON structure in localStorage.

---

### Column
**Definition:** A vertical lane on the board representing a workflow stage. The app has exactly three fixed columns: **To Do**, **In Progress**, and **Done**.

**Context:** Columns follow a left-to-right progression mirroring a Kanban workflow. Tasks move from To Do → In Progress → Done (though any direction is allowed by the UI).

**Important:** Column names are not customizable in MVP. This is listed as an open question in the PRD. Do not implement custom column names.

---

### Task
**Definition:** A single work item with a required **title** and an optional **description**. Tasks live inside a column on a board.

**Context:** Tasks are the atomic unit of work. A task belongs to exactly one column on exactly one board at any given time. Tasks can be created, edited inline, moved between columns, reordered within a column, and deleted.

**Constraints:**
- ≤ 100 tasks per board
- Title is required (non-empty after trimming)
- Description is optional
- No due dates, labels, or priority fields in MVP (these are out of scope per PRD Section 7.2)

**Data model (conceptual):**
```ts
interface Task {
  id: string;        // Unique identifier (UUID or timestamp-based)
  title: string;     // Required, non-empty
  description?: string; // Optional
  column: ColumnType;   // "todo" | "in-progress" | "done"
  order: number;     // Position within column for ordering
}
```

---

### Task Card
**Definition:** The visual UI component that renders a single task on the board. Displays the task title, and optionally the description. Supports drag-and-drop, inline editing, and keyboard interactions.

**Context:** Task cards are the primary interactive element. Users drag them between columns, click to edit inline, and use keyboard shortcuts to navigate/move/delete them.

---

### Drag-and-Drop
**Definition:** The interaction pattern where a user clicks and holds a task card, drags it to another column (or another position within the same column), and releases it to move or reorder the task.

**Context:** This is the primary method for moving tasks through workflow stages. It must provide visual feedback (drag ghost, drop target highlighting) and complete in under 100ms. A keyboard-accessible alternative (shortcut key `M`) must exist for accessibility compliance.

---

### Keyboard Shortcuts
**Definition:** Single-key commands that allow power users to manage tasks without using the mouse.

**Shortcuts defined in PRD:**
| Key | Action |
|-----|--------|
| `N` | Create a new task (opens task input) |
| `J` | Navigate to the next task |
| `K` | Navigate to the previous task |
| `M` | Move the currently selected task to the next column |
| `D` | Delete the currently selected task (with confirmation) |
| `?` | Display the keyboard shortcut help overlay |

**Context:** Keyboard shortcuts are essential for Alex's workflow — the goal is create + move + delete in under 10 seconds without touching the mouse. Shortcuts must not fire when the user is typing in an input field.

---

### localStorage Persistence
**Definition:** The mechanism by which all application data (boards, tasks, ordering) is saved to the browser's `localStorage` API as JSON.

**Context:** There is no backend. localStorage is the only persistence layer. Data is written on every state change and read on app initialization.

**Business rules:**
- All state changes must persist immediately (synchronous write)
- On page reload, the app must restore the exact previous state
- If localStorage is full (`QuotaExceededError`), show a clear error message to the user
- If stored JSON is corrupted/unparseable, fall back to empty default state (do not crash)
- Total storage must not exceed 5MB

---

### Inline Editing
**Definition:** The ability to edit a task's title and description directly on the task card without opening a separate modal or page.

**Context:** Clicking on a task's title or description transforms the text into an editable input field. Changes are saved on blur or Enter press. This keeps the workflow fast and avoids disruptive UI changes.

---

## User Personas

### Alex (Freelance Full-Stack Developer)
- Works on 2–3 client projects simultaneously
- 4 years experience, works from home and coffee shops
- Frequently offline during commutes
- Wants keyboard-driven workflow, instant task capture
- Pain: heavy tools (Jira takes 8+ seconds to load), requires internet, designed for teams not solo devs

### Maria (Computer Science Student)
- Manages coursework projects and a personal side project
- 2nd year CS student, intermittent campus Wi-Fi
- Needs clear status visibility for assignment tracking
- Pain: cloud tools require sign-ups and send notification spam, no offline access

---

## Key Business Rules

### Task Lifecycle
**Rule:** A task is created in the "To Do" column by default. It can be moved to any column in any order (To Do ↔ In Progress ↔ Done). There is no enforced linear progression.

**Rationale:** Solo developers often need flexibility — a task might jump from "To Do" directly to "Done" if it was quick, or move back from "In Progress" to "To Do" if deprioritized.

---

### Deletion Requires Confirmation
**Rule:** Deleting a task must show a confirmation prompt before the task is permanently removed. There is no undo/soft-delete in MVP.

**Rationale:** Prevents accidental data loss. The PRD's Open Questions (item #3) ask whether soft delete should be supported in the future, but MVP uses permanent deletion.

---

### Board Independence
**Rule:** Each board maintains a completely independent set of tasks. Creating, editing, moving, or deleting a task on one board must never affect any other board.

**Rationale:** Boards represent separate projects. Cross-board contamination would break the mental model.

---

### Active Board Memory
**Rule:** When the user switches between boards or reloads the page, the app must remember and restore the last active board.

**Rationale:** Prevents users from having to re-navigate to their working board on every page load.

---

## Acronyms & Jargon

| Term | Meaning |
|------|---------|
| SDD | Spec-Driven Development — the methodology this project follows |
| PRD | Product Requirements Document — defines what to build and why |
| Epic | A group of related user stories delivering end-to-end value |
| Story | A single implementable unit of work with acceptance criteria |
| ADR | Architecture Decision Record — documents technical choices |
| INVEST | Independent, Negotiable, Valuable, Estimable, Small, Testable — story quality criteria |
| WCAG | Web Content Accessibility Guidelines — accessibility standard (targeting 2.1 Level AA) |
| SPA | Single-Page Application — the architecture pattern used |
| HMR | Hot Module Replacement — Vite's instant dev server refresh |
| XSS | Cross-Site Scripting — security vulnerability prevented by React's auto-escaping |
| MVP | Minimum Viable Product — the initial scope defined in PRD Section 7.1 |