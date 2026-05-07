---
title: "Delete selected task using D key with confirmation"
type: story
status: draft
epic: "E-003"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-14"
    issue_key: "YI-14"
    issue_type: "Görev"
    parent: "YI-11"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-003.4 — Delete Task with Keyboard

<!-- INVEST Checklist (validate before finalizing)
  [x] Independent   — Can be developed and delivered without depending on another story?
  [x] Negotiable    — Is the scope flexible enough to be discussed with the team?
  [x] Valuable      — Does it deliver clear value to the user or business?
  [x] Estimable     — Does the team have enough info to size it?
  [x] Small         — Can it be completed within one sprint (≤ 5 story points / ~3 days)?
  [x] Testable      — Can acceptance criteria be verified objectively?
-->

---

## Story ID & Title

- **ID:** STORY-003.4
- **Title:** Delete selected task using D key with confirmation
- **Epic:** E-003 — Keyboard Navigation & Shortcuts
- **Priority:** [ ] Critical  [x] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to press `D` to delete the selected task with a confirmation step**
> so that **I can clean up my board without using the mouse while being protected from accidental deletions**.

---

## Acceptance Criteria

1. **Given** a task is selected, **When** I press `D`, **Then** a confirmation dialog appears with the message "Delete [task title]?" and focus is on the confirm button.
2. **Given** the delete confirmation dialog is showing, **When** I press Enter, **Then** the task is deleted and focus moves to the next task in the column.
3. **Given** the delete confirmation dialog is showing, **When** I press Escape, **Then** the dialog closes and the task remains selected and unchanged.
4. **Given** no task is selected, **When** I press `D`, **Then** nothing happens and no error or dialog appears.
5. **Given** I delete the only task in a column, **When** the deletion completes, **Then** focus moves to the first task of the next non-empty column (or clears selection if no tasks remain).

---

## Technical Notes

- Reuse the confirmation dialog component from STORY-001.4
- Manage focus carefully: dialog → task or empty state after deletion
- The `D` shortcut must be suppressed when any input/textarea/modal is focused
- Deletion must persist to localStorage immediately

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 2              |
| Estimated Days  | 1 day          |
| Assigned To     | Unassigned     |
| Sprint / Iteration | Sprint 3    |

---

## Definition of Done

- [x] Acceptance criteria all pass
- [ ] Code reviewed and approved
- [ ] Unit / integration tests written and green
- [ ] No new lint or build errors introduced
- [ ] Feature documented (if user-facing)
- [ ] Deployed to staging and verified
