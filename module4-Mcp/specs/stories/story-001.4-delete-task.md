---
title: "Delete a task with confirmation"
type: story
status: draft
epic: "E-001"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-25"
    issue_key: "YI-25"
    issue_type: "Görev"
    parent: "YI-12"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-001.4 — Delete a Task

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

- **ID:** STORY-001.4
- **Title:** Delete a task with confirmation
- **Epic:** E-001 — Core Task Management
- **Priority:** [ ] Critical  [x] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to delete a task with a confirmation step**
> so that **I can remove completed or irrelevant tasks while being protected from accidental deletion**.

---

## Acceptance Criteria

1. **Given** a task card exists on the board, **When** I click the delete button on the task card, **Then** a confirmation dialog appears asking "Are you sure you want to delete this task?".
2. **Given** the confirmation dialog is displayed, **When** I click "Confirm" or press Enter, **Then** the task is removed from the board and deleted from localStorage.
3. **Given** the confirmation dialog is displayed, **When** I click "Cancel" or press Escape, **Then** the dialog closes and the task remains unchanged.
4. **Given** I delete the last task in a column, **When** the deletion is confirmed, **Then** the column shows the empty state message and the column task count updates to 0.

---

## Technical Notes

- Use a custom modal/dialog rather than `window.confirm()` for consistent styling
- Remove task from the localStorage array by `id`
- Update column task counts after deletion
- Consider focus management: after deletion, focus moves to the next task or column

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 2              |
| Estimated Days  | 1 day          |
| Assigned To     | Unassigned     |
| Sprint / Iteration | Sprint 1    |

---

## Definition of Done

- [x] Acceptance criteria all pass
- [ ] Code reviewed and approved
- [ ] Unit / integration tests written and green
- [ ] No new lint or build errors introduced
- [ ] Feature documented (if user-facing)
- [ ] Deployed to staging and verified
