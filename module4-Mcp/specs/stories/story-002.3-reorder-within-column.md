---
title: "Reorder tasks within the same column by dragging"
type: story
status: draft
epic: "E-002"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-6"
    issue_key: "YI-6"
    issue_type: "Görev"
    parent: "YI-5"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-002.3 — Reorder Tasks Within Column

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

- **ID:** STORY-002.3
- **Title:** Reorder tasks within the same column by dragging
- **Epic:** E-002 — Drag-and-Drop Interaction
- **Priority:** [ ] Critical  [ ] High  [x] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to reorder tasks within a column by dragging them up or down**
> so that **I can prioritize my work visually by putting the most important tasks at the top**.

---

## Acceptance Criteria

1. **Given** a column has 3+ tasks, **When** I drag a task card and hover between two other cards in the same column, **Then** an insertion indicator appears showing where the card will be placed.
2. **Given** I am dragging a task within the same column, **When** I drop it between two other tasks, **Then** the task is inserted at that position and other tasks shift accordingly.
3. **Given** I reorder tasks within a column, **When** I refresh the browser, **Then** the tasks remain in the new order (order persisted to localStorage).
4. **Given** a column has only one task, **When** I try to drag it within the same column, **Then** nothing happens — the task stays in place without errors.

---

## Technical Notes

- Track an `order` or `position` field per task for stable ordering
- Recalculate order values for affected tasks on reorder
- Show insertion line/gap between cards as the drag position indicator
- Consider fractional ordering (e.g., 1.5 between 1 and 2) to minimize recalculations

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 3              |
| Estimated Days  | 2 days         |
| Assigned To     | Unassigned     |
| Sprint / Iteration | Sprint 2    |

---

## Definition of Done

- [x] Acceptance criteria all pass
- [ ] Code reviewed and approved
- [ ] Unit / integration tests written and green
- [ ] No new lint or build errors introduced
- [ ] Feature documented (if user-facing)
- [ ] Deployed to staging and verified
