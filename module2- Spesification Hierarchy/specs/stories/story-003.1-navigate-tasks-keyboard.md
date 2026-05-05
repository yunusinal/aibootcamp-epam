# User Story: STORY-003.1 — Navigate Tasks with Keyboard

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

- **ID:** STORY-003.1
- **Title:** Navigate between tasks using J/K keys
- **Epic:** E-003 — Keyboard Navigation & Shortcuts
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to navigate between task cards using `J` (down) and `K` (up) keys**
> so that **I can select tasks without reaching for the mouse during coding sessions**.

---

## Acceptance Criteria

1. **Given** the board is displayed and no task is selected, **When** I press `J`, **Then** the first task in the first non-empty column becomes selected with a visible focus indicator.
2. **Given** a task is selected, **When** I press `J`, **Then** the next task below becomes selected (wrapping to the first task of the next column when at the bottom).
3. **Given** a task is selected, **When** I press `K`, **Then** the previous task above becomes selected (wrapping to the last task of the previous column when at the top).
4. **Given** a task is selected, **When** I look at the card, **Then** it has a clearly visible focus ring/border that meets 4.5:1 contrast ratio against the background.
5. **Given** an input field or modal is focused, **When** I press `J` or `K`, **Then** the navigation shortcuts are suppressed (keys type normally in the input).

---

## Technical Notes

- Maintain a `selectedTaskId` in component state
- Use a global keydown listener that checks `document.activeElement` to avoid conflicts with inputs
- Focus indicator can be a CSS box-shadow or outline on the selected card
- Navigation order: top-to-bottom within columns, left-to-right across columns

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 3              |
| Estimated Days  | 2 days         |
| Assigned To     | Unassigned     |
| Sprint / Iteration | Sprint 3    |

---

## Definition of Done

- [x] Acceptance criteria all pass
- [ ] Code reviewed and approved
- [ ] Unit / integration tests written and green
- [ ] No new lint or build errors introduced
- [ ] Feature documented (if user-facing)
- [ ] Deployed to staging and verified
