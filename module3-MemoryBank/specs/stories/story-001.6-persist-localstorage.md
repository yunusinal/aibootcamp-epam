# User Story: STORY-001.6 — Persist Data to LocalStorage

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

- **ID:** STORY-001.6
- **Title:** Persist and restore tasks from localStorage
- **Epic:** E-001 — Core Task Management
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Maria, the Computer Science Student**,
> I want **my tasks to be automatically saved and restored when I reopen the browser**
> so that **I never lose my task data between study sessions**.

---

## Acceptance Criteria

1. **Given** I have created tasks on the board, **When** I close the browser tab and reopen it, **Then** all tasks appear in the same columns and order as when I left.
2. **Given** localStorage is empty (first visit), **When** the app loads, **Then** the board displays with three empty columns and no errors in the console.
3. **Given** localStorage contains corrupted data (invalid JSON), **When** the app loads, **Then** the app displays an empty board and logs a warning rather than crashing.
4. **Given** localStorage is full (5MB limit reached), **When** I try to create a new task, **Then** a clear error message is displayed: "Storage is full. Please delete some tasks to continue."
5. **Given** I perform any action (create, edit, delete, move), **When** the action completes, **Then** localStorage is updated within 50ms with the current state.

---

## Technical Notes

- Use a custom `useLocalStorage` hook or service module for encapsulated read/write logic
- Wrap `JSON.parse` in try/catch to handle corrupted data gracefully
- Wrap `localStorage.setItem` in try/catch to handle QuotaExceededError
- Consider a simple versioning field in the stored schema for future migrations

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
