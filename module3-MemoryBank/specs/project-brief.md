# Project Brief: Personal Task Board

## One-Liner
A lightweight, browser-only Kanban board for solo developers who need fast, offline task management without the overhead of enterprise tools.

## Background
Solo developers and CS students juggling 2–3 concurrent projects waste 15–20 minutes daily switching between heavyweight tools like Jira, Trello, and Notion — or resorting to scattered sticky notes and text files. These tools require accounts, internet connectivity, and offer features designed for large teams that add cognitive load without value for individual users.

We need a zero-setup, instant-load task board that lives entirely in the browser with no sign-ups, no subscriptions, and no backend.

## Target Users
1. **Freelance developers** working on multiple client projects who need quick task capture without leaving their coding flow
2. **CS students** managing coursework assignments and side projects on laptops with unreliable Wi-Fi

## Core Problem
- 30% of tasks fall through the cracks due to scattered tracking
- Cloud tools require internet and take 8+ seconds to load
- Existing tools demand team setup, accounts, and configuration even for solo use
- No offline-first, keyboard-friendly, lightweight alternative exists

## Desired Outcome
A single-page React application (frontend only, no backend) that allows users to:
- Create, edit, move, and delete tasks on a Kanban board (To Do → In Progress → Done)
- Drag and drop tasks between columns
- Manage multiple project boards
- Use keyboard shortcuts for all primary actions
- Work 100% offline with data stored in localStorage

## Key Constraints
- **No backend** — all data persists in browser localStorage
- **No external dependencies at runtime** — no CDNs, no analytics, no network requests
- **Tech stack:** React 18 + Vite + TypeScript (strict mode)
- **Styling:** CSS Modules or plain CSS only (no UI libraries like MUI or Tailwind)
- **Performance:** Initial render ≤ 500ms with 50 tasks
- **Accessibility:** WCAG 2.1 Level AA compliance
- **Browser support:** Last 2 versions of Chrome, Firefox, Safari, Edge

## Success Looks Like
- First task created within 30 seconds of opening the app
- Full keyboard workflow (create + move + delete) in under 10 seconds
- Zero data loss across browser sessions
- 100% offline functionality after initial load
- Supports up to 100 tasks per board and 10 boards without degradation

## Out of Scope (for MVP)
- User accounts or authentication
- Real-time collaboration
- Mobile layout (below 768px)
- Task due dates, labels, or priorities
- Import/export
- Dark mode or theming
