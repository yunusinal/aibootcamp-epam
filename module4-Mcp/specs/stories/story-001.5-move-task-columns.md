---
title: "Move a task between columns via buttons"
type: story
status: draft
epic: "E-001"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-30"
    issue_key: "YI-30"
    issue_type: "Görev"
    parent: "YI-12"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-001.5 — Move Task Between Columns

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

- **ID:** STORY-001.5
- **Title:** Move a task between columns via buttons
- **Epic:** E-001 — Core Task Management
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to move a task from one column to another using action buttons**
> so that **I can update task progress as I work through my workflow**.

---

## Acceptance Criteria

1. **Given** a task is in the "To Do" column, **When** I click the "Move to In Progress" button on the task card, **Then** the task moves to the "In Progress" column and disappears from "To Do".
2. **Given** a task is in the "In Progress" column, **When** I click the "Move to Done" button, **Then** the task moves to the "Done" column and the column counts update for both columns.
3. **Given** a task is in the "Done" column, **When** I view the task card, **Then** I see a "Move to To Do" button to restart the workflow if needed.
4. **Given** I move a task to a new column, **When** I refresh the browser, **Then** the task remains in the column I moved it to (persisted to localStorage).
5. **Given** a task is in the "To Do" column, **When** I view the task card, **Then** there is no "Move Left" button since "To Do" is the first column.

---

## Technical Notes

- Each task card shows contextual move buttons based on current column
- Update the task's `column` field in the data model
- Persist immediately to localStorage on move
- Task appears at the bottom of the destination column

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
