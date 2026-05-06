# User Story: STORY-004.3 — Delete a Board

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

- **ID:** STORY-004.3
- **Title:** Delete a board with confirmation
- **Epic:** E-004 — Multi-Board Support
- **Priority:** [ ] Critical  [x] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Maria, the Computer Science Student**,
> I want **to delete a board I no longer need with a confirmation step**
> so that **I can keep my board list clean while being protected from accidentally losing all tasks in a board**.

---

## Acceptance Criteria

1. **Given** I have multiple boards, **When** I click the delete button on a board in the selector, **Then** a confirmation dialog appears stating "Delete [board name]? All tasks in this board will be permanently removed."
2. **Given** the confirmation dialog is showing, **When** I confirm, **Then** the board and all its tasks are removed from localStorage and the selector updates.
3. **Given** I delete the currently active board, **When** the deletion completes, **Then** the view switches to another existing board automatically.
4. **Given** I have only one board remaining, **When** I try to delete it, **Then** the delete action is disabled or blocked with a message "Cannot delete the last board."
5. **Given** I delete a board, **When** I look at localStorage, **Then** both the board entry and its associated tasks key are removed.

---

## Technical Notes

- Remove both the board from the boards list and the `tasks-{boardId}` key from localStorage
- Prevent deletion of the last remaining board to avoid an empty app state
- After deleting the active board, switch to the first remaining board in the list
- Reuse the confirmation dialog component from task deletion

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 2              |
| Estimated Days  | 1 day          |
| Assigned To     | Unassigned     |
| Sprint / Iteration | Sprint 4    |

---

## Definition of Done

- [x] Acceptance criteria all pass
- [ ] Code reviewed and approved
- [ ] Unit / integration tests written and green
- [ ] No new lint or build errors introduced
- [ ] Feature documented (if user-facing)
- [ ] Deployed to staging and verified
