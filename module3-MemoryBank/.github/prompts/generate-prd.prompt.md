---
description: 'Generate a PRD from project brief'
mode: 'agent'
---

## Task

Using the PRD template in `specs/templates/prd-template.md`, create a complete PRD from the project brief provided below.

## Instructions

1. **Read the template** at `specs/templates/prd-template.md` to understand the required structure.
2. **Analyze the project brief** provided by the user (below or in conversation).
3. **Generate a full PRD** that fills in every section of the template with specific, measurable, actionable content — not generic placeholders.

## Requirements for Generated Content

- **Problem Statement:** Must include at least one quantified pain point (e.g., "users spend 15 minutes per day on manual task X").
- **Personas:** Give each persona a real name (e.g., "Sarah, the Project Manager") with concrete goals and frustrations.
- **Goals:** Must be measurable — include numbers, percentages, or timeframes.
- **Use Cases:** Write 2–4 realistic scenarios with clear preconditions and outcomes.
- **Functional Requirements:** Write testable "shall" statements. Each must be verifiable by a developer or QA engineer.
- **Non-Functional Requirements:** Include performance targets, browser support, and accessibility standards relevant to the tech stack (React 18 + Vite, localStorage, no backend).
- **Success Metrics:** Every metric must be SMART (Specific, Measurable, Achievable, Relevant, Time-bound) with baseline and target values.
- **Scope:** Explicitly list what is in scope AND out of scope. Be concrete — no vague statements.

## Output

Save the generated PRD to:

```
specs/prds/prd-{feature-name}.md
```

Use a lowercase, hyphen-separated slug derived from the project name (e.g., `prd-task-board.md`).

## Quality Checklist

Before finalizing, verify:

- [ ] Problem statement includes quantified impact (numbers, not adjectives)
- [ ] All personas have real names and specific pain points
- [ ] Goals are measurable with clear success criteria
- [ ] Success metrics follow SMART format (baseline → target, with method)
- [ ] Scope section has both "In Scope" and "Out of Scope" with concrete items
- [ ] Functional requirements use "shall" and are individually testable
- [ ] No placeholder text like `[FILL IN]` or `[TBD]` remains in the output
- [ ] File is saved to `specs/prds/` with correct naming convention

## Project Brief

{Provide your project brief here or paste it into the conversation when invoking this prompt.}
