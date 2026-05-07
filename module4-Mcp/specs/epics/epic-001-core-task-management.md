---
title: "Core Task Management"
type: epic
status: draft
epic_id: "E-001"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-12"
    issue_key: "YI-12"
    issue_type: "Epik"
    synced_at: "2026-05-11T16:42:10Z"
---

# Epic: Core Task Management

**Epic ID:** E-001
**Related PRD:** prd-task-board.md (Personal Task Board)
**Owner:** Yunus Inal
**Status:** Draft
**Sprint Target:** Q2 2026
**Last Updated:** 2026-05-05

---

## 1. Epic Title

**Core Task Management**

---

## 2. Description

This epic delivers the foundational single-board task management experience — users can create, view, edit, and delete tasks across three Kanban columns (To Do, In Progress, Done) with full localStorage persistence. It provides the essential CRUD operations and visual board layout that all other epics build upon. This is the minimum viable product that solves the core problem of lightweight task tracking for solo developers.

---

## 3. Primary Persona

**Persona:** Alex, the Freelance Full-Stack Developer

**Why they benefit:** Alex needs to capture and manage tasks instantly without tool overhead. This epic delivers a zero-setup board where tasks can be created in seconds and persist across browser sessions — eliminating the 10+ minutes daily lost to heavyweight tools.

---

## 4. Success Criteria

- [x] Users can create a new task and see it appear in the "To Do" column within 1 second
- [ ] Time to create first task is ≤ 30 seconds from initial app load
- [ ] All task data survives browser refresh with 0 data loss
- [ ] Initial board renders with up to 50 tasks in under 500ms
- [ ] All CRUD operations complete without page reload

---

## 5. Scope / Complexity

**Size Estimate:** M

**Justification:** Covers the full CRUD lifecycle plus localStorage integration, column layout, and task count display. Requires designing the data model, building multiple UI components (board, columns, task cards, forms), and implementing persistence logic.

### What This Epic Includes
- Three-column Kanban board layout (To Do, In Progress, Done)
- Task creation with title (required) and optional description
- Inline task editing (title and description)
- Task deletion with confirmation prompt
- Task count displayed in each column header
- Move task between columns via action buttons (non-drag method)
- localStorage persistence on every state change
- Load saved tasks from localStorage on app initialization
- Empty state display when no tasks exist

### What This Epic Does NOT Include
- Drag-and-drop interactions (Epic 002)
- Keyboard shortcuts (Epic 003)
- Multiple boards or board switching (Epic 004)
- Task reordering within a column
- Due dates, labels, or priority fields
- Import/export functionality

---

## 6. Dependencies

| # | Dependency                          | Type       | Status  | Owner       |
|---|-------------------------------------|------------|---------|-------------|
| 1 | React + Vite project scaffolding    | Technical  | Pending | Dev Team    |
| 2 | TypeScript data model design        | Technical  | Pending | Dev Team    |
| 3 | No external epic dependencies       | Epic       | N/A     | N/A         |

---

## 7. User Stories

> Stories have not been defined yet. Add links below as stories are written and groomed.

| Story ID  | Title                              | Status          | Link            |
|-----------|------------------------------------|-----------------|-----------------|

---

## Success Metric Mapping

| PRD Metric                    | How This Epic Contributes                              |
|-------------------------------|--------------------------------------------------------|
| Time to create first task ≤ 30s | Delivers the task creation flow directly              |
| Initial load time ≤ 500ms    | Implements the board rendering and data loading        |
| localStorage data integrity   | Implements all persistence read/write logic            |
