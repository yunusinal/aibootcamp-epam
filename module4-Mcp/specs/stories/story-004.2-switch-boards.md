---
title: "Switch between existing boards"
type: story
status: draft
epic: "E-004"
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-19"
    issue_key: "YI-19"
    issue_type: "Görev"
    parent: "YI-13"
    synced_at: "2026-05-11T16:42:10Z"
---

# User Story: STORY-004.2 — Switch Between Boards

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

- **ID:** STORY-004.2
- **Title:** Switch between existing boards
- **Epic:** E-004 — Multi-Board Support
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Maria, the Computer Science Student**,
> I want **to switch between my boards by selecting one from a list**
> so that **I can quickly move between project contexts without losing data in either board**.

---

## Acceptance Criteria

1. **Given** I have 3 boards created, **When** I look at the board selector, **Then** I see all 3 board names listed with the active board visually highlighted.
2. **Given** I am viewing "Board A", **When** I click on "Board B" in the selector, **Then** the view switches to show Board B's tasks within 200ms.
3. **Given** I switch from Board A to Board B, **When** I switch back to Board A, **Then** Board A's tasks are exactly as I left them (no data mixing).
4. **Given** I have tasks in Board A, **When** I switch to Board B and create a task there, **Then** that task does not appear in Board A.

---

## Technical Notes

- Store `activeBoardId` in localStorage so the last-viewed board loads on app restart
- Board switching loads tasks from the board-specific localStorage key
- Board selector can be a sidebar, dropdown, or tab bar — UI is negotiable
- Ensure state reset is clean when switching: clear selected task, scroll position, etc.

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
