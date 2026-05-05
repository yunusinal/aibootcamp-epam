# User Story: STORY-003.5 — Keyboard Shortcut Help Overlay

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

- **ID:** STORY-003.5
- **Title:** Show keyboard shortcut help overlay with ? key
- **Epic:** E-003 — Keyboard Navigation & Shortcuts
- **Priority:** [ ] Critical  [ ] High  [x] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Maria, the Computer Science Student**,
> I want **to press `?` to see a list of all available keyboard shortcuts**
> so that **I can discover and learn the shortcuts without memorizing them first**.

---

## Acceptance Criteria

1. **Given** the board is displayed and no input is focused, **When** I press `?`, **Then** a modal overlay appears listing all keyboard shortcuts with their descriptions.
2. **Given** the shortcut help overlay is open, **When** I press `?` again or press Escape, **Then** the overlay closes and focus returns to the board.
3. **Given** the shortcut help overlay is open, **When** I look at the content, **Then** I see at minimum: `N` (new task), `J`/`K` (navigate), `M` (move), `D` (delete), `?` (help).
4. **Given** the shortcut help overlay is open, **When** I press any other shortcut key (e.g., `N`, `J`), **Then** the shortcut is not triggered (overlay captures input).

---

## Technical Notes

- Implement as a modal/overlay component with a backdrop
- List shortcuts in a two-column layout: key on left, description on right
- Trap focus within the overlay while open (accessibility requirement)
- The `?` key requires Shift to be pressed (Shift + `/` on most keyboards) — handle appropriately

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 2              |
| Estimated Days  | 1 day          |
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
