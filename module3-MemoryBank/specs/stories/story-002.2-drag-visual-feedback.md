# User Story: STORY-002.2 — Visual Drag Feedback

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

- **ID:** STORY-002.2
- **Title:** Show visual feedback during drag operations
- **Epic:** E-002 — Drag-and-Drop Interaction
- **Priority:** [ ] Critical  [x] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to see clear visual feedback while dragging a task**
> so that **I can tell exactly where the task will land when I release it**.

---

## Acceptance Criteria

1. **Given** I start dragging a task card, **When** the drag begins, **Then** a semi-transparent ghost of the card follows my cursor within 100ms of drag start.
2. **Given** I am dragging a card, **When** I hover over a valid drop column, **Then** the column's background or border changes to indicate it will accept the drop.
3. **Given** I am dragging a card, **When** I move the cursor away from all valid columns, **Then** no column shows the drop indicator styling.
4. **Given** I start dragging a card, **When** I look at the source position, **Then** the original card shows a dimmed/placeholder state indicating it is being moved.

---

## Technical Notes

- Use CSS classes toggled via drag event handlers for drop zone highlighting
- The ghost image can use the browser's default drag image or a custom one via `setDragImage()`
- Keep visual feedback within 100ms response time per PRD non-functional requirements
- Use opacity or dashed border on the placeholder in the source column

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
