---
title: "Create a new task using the N shortcut"
type: story
status: draft
epic: "E-003"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-17"
    issue_key: "YI-17"
    issue_type: "Görev"
    parent: "YI-11"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-003.2 — Create Task with Keyboard

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

- **ID:** STORY-003.2
- **Title:** Create a new task using the N shortcut
- **Epic:** E-003 — Keyboard Navigation & Shortcuts
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to press `N` to instantly open the new task creation form**
> so that **I can capture a task idea the moment it occurs without breaking my keyboard workflow**.

---

## Acceptance Criteria

1. **Given** the board is displayed and no input is focused, **When** I press `N`, **Then** the task creation form opens with the title field automatically focused.
2. **Given** the task creation form is open via `N`, **When** I type a title and press Enter, **Then** the task is created in "To Do" and the form closes, returning focus to the new task card.
3. **Given** the task creation form is open, **When** I press Escape, **Then** the form closes without creating a task and focus returns to the previously selected task.
4. **Given** a text input or textarea is currently focused, **When** I press `N`, **Then** the character "n" is typed into the field (shortcut is suppressed).

---

## Technical Notes

- Trigger the same create form used in STORY-001.1 — reuse the component
- Use `autofocus` or `ref.focus()` to place cursor in the title field
- Track whether an input is active to suppress shortcuts during text entry
- Consider adding a brief "Task created" toast/notification for confirmation

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
