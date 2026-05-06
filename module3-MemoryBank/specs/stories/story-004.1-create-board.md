# User Story: STORY-004.1 — Create a New Board

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

- **ID:** STORY-004.1
- **Title:** Create a new named board
- **Epic:** E-004 — Multi-Board Support
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Maria, the Computer Science Student**,
> I want **to create a new board with a custom name**
> so that **I can set up a dedicated task space for each of my projects**.

---

## Acceptance Criteria

1. **Given** I am on the board view, **When** I click a "New Board" button, **Then** a form appears asking for a board name.
2. **Given** the new board form is open, **When** I enter a name and submit, **Then** a new empty board is created with three columns (To Do, In Progress, Done) and I am switched to it.
3. **Given** the new board form is open, **When** I submit without entering a name, **Then** a validation error "Board name is required" is displayed and no board is created.
4. **Given** I create a board named "Algorithm Assignment", **When** I look at the board selector, **Then** the new board appears in the list with the name I provided.
5. **Given** this is my first visit (no boards exist), **When** the app loads, **Then** a default board named "My Tasks" is automatically created and displayed.

---

## Technical Notes

- Store boards as an array of objects: `{ id, name, createdAt }`
- Each board's tasks are stored under a key like `tasks-{boardId}` in localStorage
- Board name max length: consider 50 characters
- The default "My Tasks" board should be created on first app load if no boards exist

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 3              |
| Estimated Days  | 2 days         |
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
