---
title: "Display a board selector showing all boards"
type: story
status: draft
epic: "E-004"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-20"
    issue_key: "YI-20"
    issue_type: "Görev"
    parent: "YI-13"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-004.4 — Board Selector UI

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

- **ID:** STORY-004.4
- **Title:** Display a board selector showing all boards
- **Epic:** E-004 — Multi-Board Support
- **Priority:** [ ] Critical  [x] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Maria, the Computer Science Student**,
> I want **to see a clear visual list of all my boards with the active one highlighted**
> so that **I always know which project I'm working on and can switch quickly**.

---

## Acceptance Criteria

1. **Given** I have 3 boards, **When** I look at the board selector, **Then** all 3 board names are visible with the currently active board highlighted (distinct background or border).
2. **Given** I have 10 boards (maximum per PRD), **When** I view the board selector, **Then** all boards are accessible via scrolling within the selector area without breaking the page layout.
3. **Given** no board name exceeds 50 characters, **When** I view the board selector, **Then** each board name displays without being cut off or causing layout overflow.
4. **Given** the board selector is visible, **When** I look at the "New Board" button, **Then** it is clearly distinguishable from the board list entries.

---

## Technical Notes

- Board selector can be a horizontal tab bar, vertical sidebar, or dropdown — choose based on available space
- Active board should have a distinct visual state (bold, highlight color, or underline)
- Keep the selector compact to maximize board content area
- Consider showing task count per board as a secondary indicator

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
