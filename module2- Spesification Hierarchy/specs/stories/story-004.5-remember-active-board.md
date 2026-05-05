# User Story: STORY-004.5 — Remember Last Active Board

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

- **ID:** STORY-004.5
- **Title:** Restore last active board on app reload
- **Epic:** E-004 — Multi-Board Support
- **Priority:** [ ] Critical  [ ] High  [x] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Maria, the Computer Science Student**,
> I want **the app to reopen the board I was last using when I return**
> so that **I resume my work immediately without manually navigating back to my project**.

---

## Acceptance Criteria

1. **Given** I was viewing "Algorithm Assignment" board and I close the browser, **When** I reopen the app, **Then** the "Algorithm Assignment" board is displayed automatically.
2. **Given** the previously active board has been deleted (e.g., by clearing localStorage partially), **When** the app loads, **Then** the first available board is shown instead of an error.
3. **Given** I switch from Board A to Board B, **When** I immediately refresh the page, **Then** Board B is the active board (active board ID updated on every switch).
4. **Given** this is a fresh install with no localStorage data, **When** the app loads, **Then** the default "My Tasks" board is created and set as active.

---

## Technical Notes

- Store `activeBoardId` as a separate key in localStorage (not nested inside boards data)
- On load: read `activeBoardId` → verify it exists in boards list → load that board's tasks
- Fallback chain: stored ID → first board in list → create default board
- Update `activeBoardId` in localStorage every time the user switches boards

---

## Estimation

| Field           | Value          |
|-----------------|----------------|
| Story Points    | 1              |
| Estimated Days  | 0.5 days       |
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
