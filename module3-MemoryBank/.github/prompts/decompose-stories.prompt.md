---
description: 'Break Epic into User Stories'
mode: 'agent'
---

## Task

Read an existing Epic and break it into 5–7 User Stories using the template at `specs/templates/story-template.md`.

## Instructions

1. **Read the Epic** specified by the user from `specs/epics/`.
2. **Read the story template** at `specs/templates/story-template.md`.
3. **Identify 5–7 User Stories** that together deliver the full scope of the epic.
4. **Generate each story** as a separate file following the template format.

## Story Requirements

Each story MUST:

- **Follow the standard format:** "As a [persona], I want [action] so that [benefit]"
  - Persona must match a persona from the parent PRD/Epic — use their name.
  - Action must be a single, concrete user action (not a technical task).
  - Benefit must state real user or business value.

- **Be completable in 1–3 days** by a single developer:
  - If a story feels larger than 3 days, split it further.
  - Estimate using Fibonacci story points: 1 (half day), 2 (one day), 3 (two days), 5 (three days).
  - Do NOT create stories estimated at 8+ points.

- **Have 3–5 acceptance criteria:**
  - Use Given/When/Then format.
  - Each criterion must be binary (pass/fail) — no subjective language.
  - Cover the happy path, at least one edge case, and at least one validation/error case.

- **Pass INVEST principles:**
  - **Independent** — can be developed without waiting for another story in this set.
  - **Negotiable** — describes what, not how.
  - **Valuable** — delivers something the user can see or use.
  - **Estimable** — clear enough for a developer to size confidently.
  - **Small** — fits within 1–3 days of effort.
  - **Testable** — acceptance criteria are objectively verifiable.

## Story Decomposition Strategy

When breaking down an epic, consider this ordering pattern:

1. **Foundation story** — the minimal version of the core action (create/read)
2. **Enhancement stories** — additional CRUD operations (update, delete)
3. **Validation / Error handling** — input validation, edge cases, error states
4. **UX polish** — feedback, animations, empty states, loading states
5. **Integration stories** — connecting to other features or persistence

Adjust based on the specific epic — these are guidelines, not mandatory categories.

## Output Format

Save each story as a separate file:

```
specs/stories/story-{epic-number}.{story-number}-{short-slug}.md
```

- `{epic-number}` — the zero-padded 3-digit epic number (e.g., `001`)
- `{story-number}` — sequential number within this epic (e.g., `1`, `2`, `3`)
- `{short-slug}` — lowercase, hyphen-separated, ≤ 4 words

Examples:
- `specs/stories/story-001.1-create-task.md`
- `specs/stories/story-001.2-edit-task-title.md`
- `specs/stories/story-001.3-delete-task.md`

## Quality Checklist

Before finalizing, verify each story:

- [ ] Follows "As a [named persona], I want [action] so that [benefit]" exactly
- [ ] Estimated at ≤ 5 story points (≤ 3 days of work)
- [ ] Has 3–5 acceptance criteria in Given/When/Then format
- [ ] Acceptance criteria cover: happy path + edge case + error/validation
- [ ] INVEST checklist in the comment block is all checked
- [ ] References the parent epic ID correctly
- [ ] No placeholder text remains
- [ ] Technical notes are suggestive, not prescriptive

Also verify the full set of stories:

- [ ] 5–7 stories total (if more are needed, flag for user review)
- [ ] Together they deliver the epic's full scope
- [ ] Numbered sequentially within the epic
- [ ] Minimal dependencies between stories (note any that exist)
- [ ] Priority is assigned to each story (Critical/High/Medium/Low)

## Input

Provide the path to the Epic to decompose (e.g., `specs/epics/epic-001-board-management.md`) or paste its content into the conversation.
