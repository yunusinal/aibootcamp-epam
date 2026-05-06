# Memory Banks - module3-yi

## Purpose
This memory bank provides persistent context for AI assistants working on
module3-yi (Personal Task Board) — a lightweight, frontend-only Kanban application
built with React 18 and Vite. It enables solo developers to manage tasks across
multiple projects without requiring heavyweight project management tools or
backend infrastructure. All data persists in localStorage with zero network dependency.

## Structure

### architecture/
System architecture (single-page application, client-side only), technology stack
(React 18, TypeScript strict, Vite, CSS Modules), and deployment approach (static
hosting, no backend).

### conventions/
Coding standards, naming conventions (PascalCase components, camelCase hooks/utils),
testing patterns, error handling, and quality criteria derived from the project's
Agents.MD.

### domain/
Domain-specific terminology (Board, Column, Task, drag-and-drop workflow),
business rules (task lifecycle, localStorage limits), user personas (Alex, Maria),
and key concepts unique to this Kanban board project.

### workflows/
Spec-Driven Development (SDD) process, story-by-story implementation workflow,
code review procedures, and deployment processes.

### roles/
Role-specific context for different agent roles (Product Analyst, Epic Decomposition,
Story Decomposition, Implementation, Review/QA) as defined in Agents.MD.

## Quick Navigation
- [Architecture Overview](architecture/overview.md)
- [Coding Standards](conventions/coding-standards.md)
- [Domain Glossary](domain/glossary.md)
- [Development Workflow](workflows/development-process.md)

## How to Use
When asking AI to generate code or documentation for this project, reference
the relevant memory bank files to provide context. GitHub Copilot loads these
files automatically from the workspace directory alongside the project's
`.github/copilot-instructions.md` and `agents.md`.

## Key Project Facts (Quick Reference)
- **Frontend only** — React 18 + Vite, no backend, no database
- **Language** — TypeScript in strict mode, no `any` types
- **Styling** — CSS Modules or plain CSS (no Tailwind, no MUI)
- **State** — localStorage only (no Redux, no external state libs)
- **Accessibility** — WCAG 2.1 Level AA compliance required
- **Performance** — Initial render ≤ 500ms with 50 tasks
- **Data limits** — ≤ 100 tasks per board, ≤ 10 boards, ≤ 5MB localStorage

## Maintenance
Review and update when major architectural or process changes occur.
Version control these files alongside project code.

**Last Updated:** 2026-05-06
**Version:** 1.0
