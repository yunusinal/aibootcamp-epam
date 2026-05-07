---
title: "Move selected task to next column with M key"
type: story
status: draft
epic: "E-003"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-16"
    issue_key: "YI-16"
    issue_type: "Görev"
    parent: "YI-11"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-003.3 — Move Task with Keyboard

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

- **ID:** STORY-003.3
- **Title:** Move selected task to next column with M key
- **Epic:** E-003 — Keyboard Navigation & Shortcuts
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to press `M` to move the currently selected task to the next column**
> so that **I can advance task status without using the mouse or drag-and-drop**.

---

## Acceptance Criteria

1. **Given** a task in "To Do" is selected, **When** I press `M`, **Then** the task moves to "In Progress" and the selection follows the task to its new column.
2. **Given** a task in "In Progress" is selected, **When** I press `M`, **Then** the task moves to "Done" and remains selected in the "Done" column.
3. **Given** a task in "Done" is selected, **When** I press `M`, **Then** nothing happens — the task stays in "Done" (no column beyond Done).
4. **Given** no task is selected, **When** I press `M`, **Then** nothing happens and no error is thrown.
5. **Given** I move a task via `M`, **When** I refresh the browser, **Then** the task remains in the new column (change persisted to localStorage).

---

## Technical Notes

- Column progression order: To Do → In Progress → Done (one direction only)
- Reuse the same move logic from STORY-001.5 — update `column` field and persist
- Keep the task selected after move so the user can press `M` again if needed
- Consider adding Shift+M for moving backward (Done → In Progress → To Do) in a future story

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
