# Epic: Multi-Board Support

**Epic ID:** E-004
**Related PRD:** prd-task-board.md (Personal Task Board)
**Owner:** Yunus Inal
**Status:** Draft
**Sprint Target:** Q3 2026
**Last Updated:** 2026-05-05

---

## 1. Epic Title

**Multi-Board Support**

---

## 2. Description

This epic adds the ability to create, switch between, and delete multiple independent boards. It enables developers who work across 2–3 projects to maintain separate task boards per project without data mixing. Each board operates independently with its own set of tasks and columns, directly solving the multi-project management use case defined in the PRD.

---

## 3. Primary Persona

**Persona:** Maria, the Computer Science Student

**Why they benefit:** Maria juggles multiple coursework assignments and a portfolio project simultaneously. Multi-board support lets her maintain a separate, focused task board for each project, preventing tasks from different contexts from cluttering a single view.

---

## 4. Success Criteria

- [ ] Users can create a new named board and switch to it instantly
- [ ] Switching between boards loads the correct tasks within 200ms
- [ ] Deleting a board removes it and all associated tasks from localStorage permanently
- [ ] Board data is fully isolated — actions on one board never affect another
- [ ] App supports up to 10 boards without performance degradation

---

## 5. Scope / Complexity

**Size Estimate:** S

**Justification:** Adds a board list/selector UI and extends the existing data model to namespace tasks by board ID. Core task CRUD and localStorage logic already exist from Epic 001 — this epic wraps them in a multi-board structure.

### What This Epic Includes
- Create a new board with a user-provided name
- Board selector/switcher UI showing all existing boards
- Switch between boards (loads that board's tasks)
- Delete a board with confirmation (removes board and all its tasks)
- Default board created on first app load ("My Tasks")
- Board names displayed in the switcher with active board highlighted
- localStorage schema updated to support multiple boards

### What This Epic Does NOT Include
- Board renaming or editing board properties
- Board templates or cloning an existing board
- Board-level settings (custom columns, colors)
- Drag tasks between boards
- Board ordering or sorting
- Board archiving (soft delete)

---

## 6. Dependencies

| # | Dependency                                    | Type       | Status  | Owner       |
|---|-----------------------------------------------|------------|---------|-------------|
| 1 | Core task management and localStorage (E-001) | Epic       | Pending | Dev Team    |
| 2 | Data model refactor to support board IDs      | Technical  | Pending | Dev Team    |

---

## 7. User Stories

> Stories have not been defined yet. Add links below as stories are written and groomed.

| Story ID  | Title                              | Status          | Link            |
|-----------|------------------------------------|-----------------|-----------------|

---

## Success Metric Mapping

| PRD Metric                        | How This Epic Contributes                                   |
|-----------------------------------|-------------------------------------------------------------|
| localStorage data integrity       | Extends persistence to multi-board schema without data loss |
| Initial load time ≤ 500ms        | Board switching must stay within performance budget          |
