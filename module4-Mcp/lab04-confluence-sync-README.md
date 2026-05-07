# Lab 04 — Confluence Sync (Completion Notes)

Synced a markdown PRD into Confluence via the Atlassian MCP server, then updated it.

## Environment

- **Site:** `https://yunusinal-workshop.atlassian.net`
- **Cloud ID:** `5c8f3e14-6a60-4417-aba2-9d7baf8f90b9`
- **Space:** `MCP Workshop Docs` — key `MCPDOCS`, ID `622595`

## What Was Done

| Step | Action | Result |
|------|--------|--------|
| 1 | Verified Confluence space `MCPDOCS` | Already existed (ID `622595`) |
| 2 | Created [specs/prds/PRD-001.md](specs/prds/PRD-001.md) | Markdown PRD with frontmatter |
| 3 | Created Confluence page (CREATE) | Page ID `655361`, version 1 |
| 3 | Updated PRD frontmatter with `sync.confluence.*` | URL, page_id, space_key, synced_at |
| 4 | Added FR-5: Password Strength Indicator | Local edit |
| 4 | Re-synced page (UPDATE) | Same page ID `655361`, version 2 |

## Confluence Page

- **Title:** User Authentication PRD
- **Page ID:** `655361`
- **URL:** https://yunusinal-workshop.atlassian.net/wiki/spaces/MCPDOCS/pages/655361/User+Authentication+PRD

## Frontmatter (final)

```yaml
sync:
  confluence:
    url: "https://yunusinal-workshop.atlassian.net/wiki/spaces/MCPDOCS/pages/655361/User+Authentication+PRD"
    page_id: 655361
    space_key: MCPDOCS
    synced_at: "2026-05-11T16:10:39Z"
```

## Key Takeaways

- **Markdown is source of truth**, Confluence mirrors it.
- **CREATE** returns a new `pageId`; **UPDATE** keeps the same `pageId` and bumps `version.number`.
- The Atlassian MCP converts markdown → Confluence storage HTML automatically (headings, lists, etc. preserved).
- Tracking `page_id` + `synced_at` in frontmatter enables idempotent re-syncs.
