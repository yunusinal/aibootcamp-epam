# Lab 5 — Reusable Sync Prompts

A small collection of reusable GitHub Copilot prompt files for batch syncing markdown specs to Jira and Confluence.

## What's Inside

Located in [.github/prompts/](.github/prompts):

| Prompt | Purpose |
|--------|---------|
| [sync-to-jira.prompt.md](.github/prompts/sync-to-jira.prompt.md) | Batch sync `specs/stories/` to Jira project **MCPW** with epic parent links |
| [sync-to-confluence.prompt.md](.github/prompts/sync-to-confluence.prompt.md) | Batch sync `specs/prds/` to Confluence space **MCPDOCS** |
| [check-sync-status.prompt.md](.github/prompts/check-sync-status.prompt.md) | Detect NEW / OUT-OF-DATE / UP-TO-DATE / ORPHANED files |
| [sync-plan.prompt.md](.github/prompts/sync-plan.prompt.md) | Two-way sync plan with conflict detection + approval gate |

## Prerequisites

- Labs 3–4 complete (Atlassian MCP authenticated)
- At least one markdown file in `specs/` with sync frontmatter

## How to Use

In Copilot Chat, invoke a prompt by name:

```
/sync-to-jira sync all my stories
/sync-to-confluence sync all my PRDs
/check-sync-status show me what's out of sync
/sync-plan generate a two-way sync plan
```

Each prompt follows a **Discover → Analyze → Preview → Approve → Execute → Report** flow. Nothing is pushed to Jira/Confluence without your confirmation.

## Sync State Cheat Sheet

| State | Frontmatter | Remote | Action |
|-------|-------------|--------|--------|
| 🆕 NEW | No `sync` block | — | CREATE |
| ⚠️ OUT-OF-DATE | Has `sync`, file modified after `synced_at` | Exists | UPDATE |
| ✅ UP-TO-DATE | Has `sync`, no local changes | Exists | Skip |
| ❌ ORPHANED | Has `sync` | Deleted | Clean up |
| ⚠️ CONFLICT | Both local and remote changed since `synced_at` | Exists | Merge |

## When to Use Prompts vs Inline Commands

- **Prompt files** — repeatable batch workflows, team-shared, version-controlled
- **Inline commands** — one-off syncs, quick experiments, single files

## Reference

See [lab-05-reusable-prompts.md](lab-05-reusable-prompts.md) for the full lab walkthrough.
