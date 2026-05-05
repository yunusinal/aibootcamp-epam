# User Story: STORY-002.4 — Drop Position in Target Column

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

- **ID:** STORY-002.4
- **Title:** Choose drop position when moving to another column
- **Epic:** E-002 — Drag-and-Drop Interaction
- **Priority:** [ ] Critical  [ ] High  [x] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to choose where in the target column my task lands when I drag it across columns**
> so that **I can place it at the right priority position immediately instead of moving it again**.

---

## Acceptance Criteria

1. **Given** I am dragging a task to a different column that already has tasks, **When** I hover between two tasks in the target column, **Then** an insertion indicator shows the exact drop position.
2. **Given** I drag a task to the top area of a target column, **When** I release, **Then** the task is inserted at the top of that column above all existing tasks.
3. **Given** I drag a task to the bottom area of a target column, **When** I release, **Then** the task is inserted at the bottom of that column below all existing tasks.
4. **Given** I drag a task to an empty target column, **When** I release anywhere in the column, **Then** the task becomes the only item in that column.

---

## Technical Notes

- Calculate drop index based on cursor Y position relative to existing cards
- Reuse the insertion indicator component from STORY-002.3
- Update both `column` and `order` fields on cross-column drops
- Handle edge case: dropping at the very top or very bottom of the card list

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 2              |
| Estimated Days  | 1 day          |
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
