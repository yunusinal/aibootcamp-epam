# User Story: STORY-002.1 — Drag Task Between Columns

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

- **ID:** STORY-002.1
- **Title:** Drag a task card from one column to another
- **Epic:** E-002 — Drag-and-Drop Interaction
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to drag a task card from one column and drop it into another column**
> so that **I can update task status with a single fluid gesture instead of clicking buttons**.

---

## Acceptance Criteria

1. **Given** a task card exists in "To Do", **When** I click and hold the card then drag it over the "In Progress" column, **Then** the card follows my cursor and the target column shows a visual drop indicator.
2. **Given** I am dragging a card over a valid column, **When** I release the mouse button, **Then** the task moves to the target column and disappears from the source column.
3. **Given** I start dragging a card, **When** I release it outside of any column (invalid drop zone), **Then** the card returns to its original position in the source column.
4. **Given** I drag a task to a new column, **When** the drop completes, **Then** the column task counts update immediately for both source and destination columns.
5. **Given** I drag a task to a new column, **When** I refresh the browser, **Then** the task remains in the new column (change persisted to localStorage).

---

## Technical Notes

- Consider HTML5 Drag and Drop API or a lightweight React DnD library
- Set `draggable="true"` on task card elements
- Use `onDragStart`, `onDragOver`, `onDrop` event handlers
- Persist column change to localStorage on successful drop

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 5              |
| Estimated Days  | 3 days         |
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
