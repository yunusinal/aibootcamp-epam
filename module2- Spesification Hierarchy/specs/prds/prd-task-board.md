# Product Requirements Document (PRD)

**Project:** Personal Task Board
**Author:** Yunus Inal
**Status:** Draft
**Version:** 1.0
**Last Updated:** 2026-05-05

---

## 1. Overview

### 1.1 Purpose
This document defines the product requirements for Personal Task Board — a lightweight, frontend-only Kanban application built with React and Vite. It enables solo developers to manage tasks across multiple projects without requiring heavyweight project management tools or backend infrastructure.

### 1.2 Problem Statement
Solo developers managing 2–3 concurrent projects spend an average of 15–20 minutes per day context-switching between tools (Jira, Trello, Notion) or maintaining ad-hoc task lists in text files and sticky notes. This results in:

- **30% of tasks falling through the cracks** due to scattered tracking across multiple tools
- **10+ minutes daily** lost to loading heavy project management UIs and navigating complex interfaces designed for large teams
- **No offline access** — cloud-based tools require internet connectivity, blocking task management during commutes or network outages
- **Feature overload** — 80% of Jira/Trello features are unused by solo developers, adding cognitive load without value

Developers need a zero-setup, instant-load task board that works entirely in the browser with no account creation, no subscriptions, and no backend dependencies.

### 1.3 Goals
- Reduce daily task management overhead from 15+ minutes to under 3 minutes within the first week of use
- Achieve first task creation within 30 seconds of opening the app (zero onboarding)
- Support management of up to 100 tasks across 3 projects without performance degradation
- Provide full offline functionality — 100% of features available without network connectivity
- Reach keyboard-only workflow completion (create, move, delete task) in under 10 seconds

---

## 2. User Personas

### Persona 1: Alex, the Freelance Full-Stack Developer
- **Role:** Solo developer working on 2–3 client projects simultaneously
- **Background:** 4 years of experience, works from home and coffee shops, frequently offline during commutes. Manages personal projects alongside client work.
- **Goals:** Quickly capture tasks as they arise during coding sessions; visualize progress across projects at a glance; move tasks through stages without leaving the keyboard
- **Pain Points:** Jira takes 8+ seconds to load and requires navigating 3 screens to create a task; Trello requires internet; text file lists provide no visual status overview; existing tools require team setup even for solo use

### Persona 2: Maria, the Computer Science Student
- **Role:** Student developer managing coursework projects and a personal side project
- **Background:** 2nd year CS student, works on a laptop with intermittent campus Wi-Fi. Juggles 2–3 assignment projects with deadlines plus a portfolio project.
- **Goals:** Track assignment tasks with clear status visibility; avoid forgetting subtasks before deadlines; have a distraction-free tool that doesn't require account setup
- **Pain Points:** Cloud tools require sign-ups and send notification spam; sticky notes get lost; phone reminders lack the board visualization needed to see overall progress

---

## 3. Use Cases

### UC-01: Quick Task Capture During Coding
- **Actor:** Alex (developer)
- **Precondition:** App is open in a browser tab; at least one project column exists
- **Steps:**
  1. Alex presses keyboard shortcut `N` to open new task input
  2. Types task title: "Fix auth token refresh bug"
  3. Presses Enter to confirm
  4. Task appears in "To Do" column
- **Expected Outcome:** Task is created and persisted to localStorage in under 1 second, visible in the To Do column immediately

### UC-02: Moving a Task Through Workflow Stages
- **Actor:** Alex (developer)
- **Precondition:** A task exists in the "To Do" column
- **Steps:**
  1. Alex drags the task card from "To Do" to "In Progress"
  2. The card visually moves to the new column
  3. After completing work, Alex drags the card from "In Progress" to "Done"
- **Expected Outcome:** Task position is updated in localStorage; column counts update immediately; card renders in the new column without page reload

### UC-03: Managing Multiple Projects
- **Actor:** Maria (student)
- **Precondition:** App is loaded with no existing data (first use)
- **Steps:**
  1. Maria creates a board named "Algorithm Assignment"
  2. Adds tasks: "Implement BFS", "Write unit tests", "Document complexity"
  3. Switches to create a second board: "Portfolio Site"
  4. Adds tasks for the second project
- **Expected Outcome:** Each board maintains independent task lists; switching between boards is instant; all data persists across browser sessions

### UC-04: Keyboard-Driven Task Management
- **Actor:** Alex (developer)
- **Precondition:** App is open with tasks in various columns
- **Steps:**
  1. Alex presses `J`/`K` to navigate between tasks
  2. Presses `M` to move the selected task to the next column
  3. Presses `D` to delete a completed task
  4. Confirms deletion with Enter
- **Expected Outcome:** All actions complete without mouse interaction; focus indicators show which task is selected; state persists after each action

---

## 4. Functional Requirements

> Requirements must be testable and unambiguous. Use "shall" for mandatory requirements.

| ID     | Requirement                                                                                              | Priority |
|--------|----------------------------------------------------------------------------------------------------------|----------|
| FR-01  | The system shall display tasks in three columns: "To Do", "In Progress", and "Done"                      | High     |
| FR-02  | The system shall allow users to create a new task with a title (required) and optional description        | High     |
| FR-03  | The system shall support drag-and-drop to move tasks between columns                                     | High     |
| FR-04  | The system shall persist all task data to localStorage on every state change                              | High     |
| FR-05  | The system shall load previously saved tasks from localStorage on app initialization                     | High     |
| FR-06  | The system shall allow users to delete a task with a confirmation prompt                                  | High     |
| FR-07  | The system shall allow users to edit a task's title and description inline                                | Medium   |
| FR-08  | The system shall support keyboard shortcuts: `N` (new task), `J/K` (navigate), `M` (move), `D` (delete)  | Medium   |
| FR-09  | The system shall display the count of tasks in each column header                                         | Medium   |
| FR-10  | The system shall support multiple boards, allowing users to create, switch, and delete boards             | Medium   |
| FR-11  | The system shall allow users to reorder tasks within the same column via drag-and-drop                    | Low      |
| FR-12  | The system shall display a keyboard shortcut help overlay when the user presses `?`                       | Low      |

---

## 5. Non-Functional Requirements

### 5.1 Performance
- The app shall render the initial board with up to 50 tasks in under 500ms on a mid-range laptop (Intel i5, 8GB RAM)
- Drag-and-drop operations shall complete with visual feedback in under 100ms
- localStorage read/write operations shall complete in under 50ms for datasets up to 500KB

### 5.2 Security
- The application shall not make any external network requests (no analytics, no CDNs at runtime)
- All data shall remain in the user's browser localStorage — no data leaves the device
- The app shall sanitize any user-provided text before rendering to prevent XSS via task titles or descriptions

### 5.3 Scalability
- The application shall handle up to 100 tasks per board and up to 10 boards without degraded performance
- localStorage usage shall not exceed 5MB (browser default limit)

### 5.4 Availability & Reliability
- The application shall function 100% offline after initial load (no network dependency)
- The application shall gracefully handle localStorage being full by displaying a clear error message
- The application shall not crash or lose data if the browser tab is closed mid-operation

### 5.5 Accessibility
- The UI shall conform to WCAG 2.1 Level AA standards
- All interactive elements shall be reachable via keyboard Tab navigation
- Drag-and-drop shall have a keyboard-accessible alternative (move via shortcut keys)
- Color contrast ratios shall meet at least 4.5:1 for normal text

### 5.6 Compatibility
- The application shall support the latest two major versions of Chrome, Firefox, Safari, and Edge
- The application shall be responsive and usable on viewports from 768px to 1920px width
- The application shall work on both macOS and Windows operating systems

---

## 6. Success Metrics

> Define how success will be measured after launch.

| Metric                              | Baseline              | Target                | Measurement Method                              |
|-------------------------------------|-----------------------|-----------------------|-------------------------------------------------|
| Time to create first task           | N/A (new app)         | ≤ 30 seconds         | Manual QA testing with stopwatch on first load  |
| Task move interaction time          | N/A                   | ≤ 2 seconds (drag) / ≤ 1 second (keyboard) | Performance timing in dev tools     |
| Initial load time (50 tasks)        | N/A                   | ≤ 500ms              | Lighthouse performance audit                    |
| localStorage data integrity         | N/A                   | 0 data loss incidents | Automated tests: write → reload → verify cycle  |
| Keyboard workflow completion        | N/A                   | ≤ 10 seconds for create+move+delete | Timed user testing session         |
| Accessibility compliance            | 0%                    | 100% WCAG 2.1 AA     | axe-core automated audit with 0 violations      |

---

## 7. Scope

### 7.1 In Scope
- Kanban board with three fixed columns: To Do, In Progress, Done
- Task CRUD operations (create, read, update, delete)
- Drag-and-drop task movement between columns and reordering within columns
- Keyboard shortcuts for all primary actions
- Multiple board support with board switching
- Data persistence via localStorage
- Responsive layout for desktop viewports (768px–1920px)
- Accessible UI conforming to WCAG 2.1 Level AA

### 7.2 Out of Scope
- User authentication or user accounts — no login required
- Backend API or database — all data is client-side only
- Real-time collaboration or multi-user support
- Mobile-optimized layout (below 768px viewport)
- Task due dates, labels, or priority fields (deferred to future release)
- Import/export functionality (e.g., CSV, JSON)
- Browser notifications or reminders
- Dark mode or theme customization

### 7.3 Future Considerations
- Task labels and color coding for categorization
- Due dates with optional browser notification reminders
- JSON export/import for backup and portability
- Dark mode / theme toggle
- Sub-tasks or checklist items within a task
- Mobile-responsive layout for viewports below 768px

---

## Appendix

### Open Questions
| # | Question                                                      | Owner   | Due Date   | Status |
|---|---------------------------------------------------------------|---------|------------|--------|
| 1 | Should boards support custom column names beyond the default three? | Product | 2026-05-12 | Open   |
| 2 | What is the maximum task title length before truncation?       | Design  | 2026-05-12 | Open   |
| 3 | Should deleted tasks be recoverable (soft delete) or permanent? | Product | 2026-05-12 | Open   |

### Revision History
| Version | Date       | Author      | Summary of Changes |
|---------|------------|-------------|--------------------|
| 1.0     | 2026-05-05 | Yunus Inal  | Initial draft      |
