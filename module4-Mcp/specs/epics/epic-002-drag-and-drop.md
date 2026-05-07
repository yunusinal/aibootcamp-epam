---
title: "Drag-and-Drop Interaction"
type: epic
status: draft
epic_id: "E-002"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-5"
    issue_key: "YI-5"
    issue_type: "Epik"
    synced_at: "2026-05-11T16:42:10Z"
---

# Epic: Drag-and-Drop Interaction

**Epic ID:** E-002
**Related PRD:** prd-task-board.md (Personal Task Board)
**Owner:** Yunus Inal
**Status:** Draft
**Sprint Target:** Q2 2026
**Last Updated:** 2026-05-05

---

## 1. Epic Title

**Drag-and-Drop Interaction**

---

## 2. Description

This epic adds drag-and-drop functionality for moving tasks between columns and reordering tasks within a column. It transforms the board from a button-driven interface into an intuitive, visual task management experience that matches users' mental model of physically moving cards. This directly reduces task movement time and provides the fluid Kanban experience developers expect.

---

## 3. Primary Persona

**Persona:** Alex, the Freelance Full-Stack Developer

**Why they benefit:** Alex moves tasks through workflow stages multiple times per day. Drag-and-drop reduces the cognitive and physical effort to move a task from 2–3 clicks to a single gesture, keeping Alex in flow state during coding sessions.

---

## 4. Success Criteria

- [ ] Users can drag a task card from one column and drop it into another column
- [ ] Drag-and-drop visual feedback (ghost card, drop indicators) appears within 100ms of drag start
- [ ] Users can reorder tasks within the same column by dragging
- [ ] New positions persist to localStorage immediately after drop
- [ ] Drag-and-drop works on latest Chrome, Firefox, Safari, and Edge

---

## 5. Scope / Complexity

**Size Estimate:** S

**Justification:** Focused on a single interaction pattern (drag-and-drop). Leverages existing task data model and localStorage logic from Epic 001. Requires implementing HTML5 drag-and-drop or a React DnD solution.

### What This Epic Includes
- Drag task cards between the three columns (To Do, In Progress, Done)
- Visual feedback during drag: ghost card following cursor
- Drop zone indicators showing valid drop targets
- Reorder tasks within the same column via drag-and-drop
- Position persistence to localStorage after each drop
- Accessible drop feedback (ARIA live region announcement)

### What This Epic Does NOT Include
- Keyboard-based task movement (Epic 003)
- Touch/mobile drag interactions (out of scope per PRD)
- Drag to create new tasks
- Multi-select drag (moving multiple tasks at once)
- Animation or spring physics on drop

---

## 6. Dependencies

| # | Dependency                                    | Type       | Status  | Owner       |
|---|-----------------------------------------------|------------|---------|-------------|
| 1 | Core board layout and task cards (Epic 001)   | Epic       | Pending | Dev Team    |
| 2 | Task data model with position/order field     | Technical  | Pending | Dev Team    |

---

## 7. User Stories

> Stories have not been defined yet. Add links below as stories are written and groomed.

| Story ID  | Title                              | Status          | Link            |
|-----------|------------------------------------|-----------------|-----------------|

---

## Success Metric Mapping

| PRD Metric                         | How This Epic Contributes                              |
|------------------------------------|--------------------------------------------------------|
| Task move interaction time ≤ 2s    | Drag-and-drop is the primary move mechanism measured   |
| Accessibility compliance (WCAG AA) | Includes ARIA announcements for drag actions           |
