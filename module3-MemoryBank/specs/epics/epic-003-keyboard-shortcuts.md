# Epic: Keyboard Navigation & Shortcuts

**Epic ID:** E-003
**Related PRD:** prd-task-board.md (Personal Task Board)
**Owner:** Yunus Inal
**Status:** Draft
**Sprint Target:** Q2 2026
**Last Updated:** 2026-05-05

---

## 1. Epic Title

**Keyboard Navigation & Shortcuts**

---

## 2. Description

This epic implements full keyboard-driven task management, enabling power users to create, navigate, move, and delete tasks without touching the mouse. It includes a discoverable shortcut help overlay and visible focus indicators. This directly addresses the PRD goal of completing a full keyboard workflow (create → move → delete) in under 10 seconds.

---

## 3. Primary Persona

**Persona:** Alex, the Freelance Full-Stack Developer

**Why they benefit:** Alex works primarily from the keyboard during coding sessions. Switching to the mouse for task management breaks flow state. Keyboard shortcuts allow Alex to capture and organize tasks in seconds without leaving the keyboard, reducing context-switch overhead.

---

## 4. Success Criteria

- [ ] Users can create a task, move it to another column, and delete it using only keyboard shortcuts in ≤ 10 seconds
- [ ] All interactive elements are reachable via Tab navigation
- [ ] Focus indicators are clearly visible on the currently selected task (meets 4.5:1 contrast)
- [ ] Pressing `?` displays the keyboard shortcut help overlay
- [ ] Shortcuts do not conflict with browser default shortcuts

---

## 5. Scope / Complexity

**Size Estimate:** S

**Justification:** Focused set of keyboard bindings with clear scope. Requires event listeners, focus management, and a simple overlay component. No new data model work needed.

### What This Epic Includes
- Keyboard shortcut `N` to open new task creation input
- Shortcuts `J`/`K` to navigate between tasks (down/up)
- Shortcut `M` to move selected task to the next column
- Shortcut `D` to delete the selected task (with confirmation)
- Visible focus indicator on the currently selected task card
- `?` shortcut to toggle keyboard shortcut help overlay
- Tab-based navigation through all interactive elements
- ARIA roles and labels for screen reader compatibility

### What This Epic Does NOT Include
- Drag-and-drop interactions (Epic 002)
- Custom keybinding configuration by users
- Vim-style multi-key commands (e.g., `dd` to delete)
- Shortcut customization or remapping
- Touch gestures or swipe actions

---

## 6. Dependencies

| # | Dependency                                    | Type       | Status  | Owner       |
|---|-----------------------------------------------|------------|---------|-------------|
| 1 | Core board layout and task cards (Epic 001)   | Epic       | Pending | Dev Team    |
| 2 | Task selection state management               | Technical  | Pending | Dev Team    |

---

## 7. User Stories

> Stories have not been defined yet. Add links below as stories are written and groomed.

| Story ID  | Title                              | Status          | Link            |
|-----------|------------------------------------|-----------------|-----------------|

---

## Success Metric Mapping

| PRD Metric                              | How This Epic Contributes                                  |
|-----------------------------------------|------------------------------------------------------------|
| Keyboard workflow completion ≤ 10s      | Directly delivers the keyboard workflow measured            |
| Accessibility compliance (WCAG 2.1 AA) | Implements keyboard accessibility and focus management      |
| Task move interaction time ≤ 1s (kbd)  | Keyboard move shortcut is the measured interaction          |
