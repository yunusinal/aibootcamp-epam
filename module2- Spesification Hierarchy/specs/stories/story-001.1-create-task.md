# User Story: STORY-001.1 — Create a New Task

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

- **ID:** STORY-001.1
- **Title:** Create a new task on the board
- **Epic:** E-001 — Core Task Management
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to create a new task with a title and optional description**
> so that **I can quickly capture work items without losing my train of thought**.

---

## Acceptance Criteria

1. **Given** the board is displayed, **When** I click the "Add Task" button in the "To Do" column, **Then** a task creation form appears with a title input field and an optional description field.
2. **Given** the task creation form is open, **When** I enter a title and press Enter or click "Save", **Then** a new task card appears at the bottom of the "To Do" column with the entered title.
3. **Given** the task creation form is open, **When** I submit the form without a title, **Then** the form displays a validation error "Title is required" and does not create a task.
4. **Given** a task with a title of 200 characters, **When** I submit the form, **Then** the task is created and the title is displayed (truncated visually if needed but stored in full).
5. **Given** I have created a task, **When** I refresh the browser, **Then** the task still appears in the "To Do" column (persisted to localStorage).

---

## Technical Notes

- Store tasks as an array of objects in localStorage keyed by board ID
- Each task needs: `id` (UUID), `title`, `description`, `column`, `createdAt`, `order`
- Sanitize user input before rendering to prevent XSS
- Consider using `crypto.randomUUID()` for task IDs

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 3              |
| Estimated Days  | 2 days         |
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
