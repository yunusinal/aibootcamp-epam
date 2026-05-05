# User Story: STORY-001.2 — View Board with Columns

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

- **ID:** STORY-001.2
- **Title:** View the Kanban board with three columns
- **Epic:** E-001 — Core Task Management
- **Priority:** [x] Critical  [ ] High  [ ] Medium  [ ] Low
- **Status:** [x] Draft  [ ] Ready  [ ] In Progress  [ ] Done

---

## User Story

> As **Alex, the Freelance Full-Stack Developer**,
> I want **to see my tasks organized in three columns (To Do, In Progress, Done)**
> so that **I can visualize my workflow status at a glance without navigating multiple screens**.

---

## Acceptance Criteria

1. **Given** I open the application, **When** the page loads, **Then** I see three columns labeled "To Do", "In Progress", and "Done" displayed side by side.
2. **Given** tasks exist in localStorage, **When** the app initializes, **Then** each task is displayed in its assigned column as a card showing the task title.
3. **Given** a column has tasks, **When** I look at the column header, **Then** I see the column name and a count of tasks in that column (e.g., "To Do (3)").
4. **Given** no tasks exist (first visit or all deleted), **When** the board loads, **Then** each column displays an empty state message (e.g., "No tasks yet").
5. **Given** a column has more tasks than fit in the viewport, **When** I scroll within the column, **Then** additional task cards become visible without affecting other columns.

---

## Technical Notes

- Board layout: CSS Grid or Flexbox with three equal-width columns
- Responsive design for viewports 768px–1920px
- Column component receives tasks filtered by column status
- Consider virtualization only if performance testing shows issues with 50+ tasks

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
