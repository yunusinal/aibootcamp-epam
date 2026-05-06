---
description: 'Decompose PRD into Epics'
mode: 'agent'
---

## Task

Read an existing PRD and decompose it into 3–4 high-level Epics using the template at `specs/templates/epic-template.md`.

## Instructions

1. **Read the PRD** specified by the user from `specs/prds/`.
2. **Read the epic template** at `specs/templates/epic-template.md`.
3. **Identify 3–4 Epics** that collectively cover the PRD's functional requirements and deliver its success metrics.
4. **Generate each Epic** as a separate file following the template format.

## Epic Decomposition Rules

Each Epic MUST:

- **Deliver end-to-end value** — a user can accomplish a complete workflow when the epic ships. No "backend-only" or "setup-only" epics.
- **Be independently deployable** — shipping one epic does not require another epic to be complete first (minimize cross-epic dependencies).
- **Map to a Success Metric** — every epic must directly contribute to at least one success metric defined in the PRD. State which metric it maps to.
- **Have clear boundaries** — the "Includes" and "Does NOT Include" sections must be specific enough that two developers would agree on whether a task belongs to this epic.

## Decomposition Strategy

When splitting the PRD into epics, consider these natural boundaries:

1. **Core CRUD / Primary workflow** — the foundational feature that everything else builds on
2. **Organization / Management** — categorization, filtering, sorting, grouping
3. **User experience enhancements** — drag-and-drop, keyboard shortcuts, transitions, polish
4. **Data persistence / Reliability** — storage, export, import, backup, recovery

Adjust boundaries based on the specific PRD — these are guidelines, not rigid categories.

## Output Format

For each epic, save a separate file:

```
specs/epics/epic-{NNN}-{short-slug}.md
```

- Use zero-padded 3-digit numbering starting at `001`.
- Use lowercase, hyphen-separated slugs (≤ 4 words).
- Example: `specs/epics/epic-001-board-management.md`

## Quality Checklist

Before finalizing, verify each epic:

- [ ] Has a clear, action-oriented title
- [ ] Maps to at least one PRD success metric (stated explicitly)
- [ ] Delivers standalone user value — not just a technical layer
- [ ] Can be deployed independently of other epics
- [ ] "Includes" and "Does NOT Include" lists are concrete (no vague items)
- [ ] Size estimate is S or M (if L, split further)
- [ ] No placeholder text remains — all sections filled with specific content
- [ ] Persona references match those defined in the PRD

Also verify the full set of epics:

- [ ] Together they cover all functional requirements from the PRD
- [ ] No significant overlap between epics
- [ ] Numbered sequentially (001, 002, 003…)
- [ ] Dependencies between epics are minimal and documented

## Input

Provide the path to the PRD to decompose (e.g., `specs/prds/prd-task-board.md`) or paste its content into the conversation.
