---
title: "Navigate all interactive elements via Tab key"
type: story
status: draft
epic: "E-003"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-29"
    issue_key: "YI-29"
    issue_type: "Görev"
    parent: "YI-11"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-003.6 — Tab Navigation for Accessibility

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

- **ID:** STORY-003.6
- **Title:** Navigate all interactive elements via Tab key
- **Epic:** E-003 — Keyboard Navigation & Shortcuts
- **Priority:** [ ] Critical  [x] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to reach every interactive element on the board using the Tab key**
> so that **I can use the full app without a mouse and the app meets accessibility standards**.

---

## Acceptance Criteria

1. **Given** the board is loaded, **When** I press Tab repeatedly, **Then** focus moves through all interactive elements in a logical order (column headers → task cards → action buttons).
2. **Given** a task card has focus, **When** I press Tab, **Then** focus moves to the action buttons within that card (edit, delete, move) before moving to the next card.
3. **Given** focus is on any interactive element, **When** I look at the element, **Then** it has a visible focus indicator (outline or ring) with at least 4.5:1 contrast ratio.
4. **Given** focus is on the last interactive element on the board, **When** I press Tab, **Then** focus wraps to the first interactive element (standard browser tab behavior).
5. **Given** I press Shift+Tab, **When** an element is focused, **Then** focus moves to the previous interactive element in reverse order.

---

## Technical Notes

- Ensure all buttons and interactive elements have proper `tabindex` (0 for natural order, -1 for programmatic only)
- Use semantic HTML elements (`<button>`, `<a>`) which are natively focusable
- Add `role` and `aria-label` attributes to task cards for screen reader context
- Test with axe-core to verify no focus-order violations

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
