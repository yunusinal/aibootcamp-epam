# User Story: STORY-002.5 — Accessible Drag Announcements

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

- **ID:** STORY-002.5
- **Title:** Announce drag-and-drop actions to screen readers
- **Epic:** E-002 — Drag-and-Drop Interaction
- **Priority:** [ ] Critical  [ ] High  [x] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **drag-and-drop actions to be announced by screen readers**
> so that **the board remains accessible and meets WCAG 2.1 AA standards even with drag interactions**.

---

## Acceptance Criteria

1. **Given** a screen reader is active, **When** I start dragging a task, **Then** the screen reader announces "Grabbed [task title] from [column name]".
2. **Given** I am dragging a task with a screen reader active, **When** I hover over a new column, **Then** the screen reader announces "Over [column name] column".
3. **Given** I drop a task in a new column, **When** the drop completes, **Then** the screen reader announces "Dropped [task title] in [column name]".
4. **Given** I cancel a drag (release in invalid zone), **When** the card returns to origin, **Then** the screen reader announces "Movement cancelled, [task title] returned to [column name]".

---

## Technical Notes

- Use an ARIA live region (`aria-live="assertive"`) for drag announcements
- Update the live region text content at each drag phase (grab, over, drop, cancel)
- Do not interfere with visual drag feedback — announcements are purely auditory
- Test with NVDA or VoiceOver to verify announcements are read correctly

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
