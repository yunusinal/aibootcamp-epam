# User Story: STORY-001.3 — Edit Task Inline

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

- **ID:** STORY-001.3
- **Title:** Edit a task's title and description inline
- **Epic:** E-001 — Core Task Management
- **Priority:** [ ] Critical  [x] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to edit a task's title and description by clicking on it**
> so that **I can fix typos or update task details without deleting and recreating the task**.

---

## Acceptance Criteria

1. **Given** a task card exists on the board, **When** I click on the task title, **Then** the title becomes an editable text input pre-filled with the current title.
2. **Given** I am editing a task title, **When** I change the text and press Enter or click outside, **Then** the task title updates to the new value and the change persists to localStorage.
3. **Given** I am editing a task title, **When** I clear the title field and try to save, **Then** the edit is rejected with a validation message and the original title is restored.
4. **Given** I am editing a task, **When** I press Escape, **Then** the edit is cancelled and the original title/description is preserved.
5. **Given** I edit a task's description, **When** I save the change, **Then** the updated description is persisted and visible when viewing the task.

---

## Technical Notes

- Inline editing can use a controlled input that toggles between display and edit mode
- Debounce localStorage writes if using onChange (or write on blur/Enter)
- Preserve task `id`, `createdAt`, and `order` when updating other fields
- Sanitize edited content before saving

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
