# Lab 03 - Jira Sync via Atlassian MCP

## Overview

This lab demonstrates how to sync markdown story files to Jira issues using the Atlassian MCP (Model Context Protocol) server. It covers the full CREATE and UPDATE sync workflow.

## What Was Done

### Prerequisites
- **Atlassian Site:** `yunusinal-workshop.atlassian.net`
- **Jira Project:** MCP Workshop (key: `YI`)
- **MCP Server:** `com.atlassian/atlassian-mcp-server` v1.1.1 configured via `.vscode/mcp.json`
- **OAuth:** Completed via Atlassian cloud

### Step 1: Created Story File
- Created `specs/stories/STORY-001.md` with YAML frontmatter and user story content
- Story: "User Login Form" with 3 acceptance criteria (AC1–AC3) and technical notes
- Frontmatter fields: `title`, `type`, `status`

### Step 2: Synced to Jira (CREATE)
- Used `mcp_com_atlassian_createJiraIssue` to create a new Feature in project `YI`
- **Result:** Issue `YI-4` created at https://yunusinal-workshop.atlassian.net/browse/YI-4
- Frontmatter updated with `sync.jira.url`, `sync.jira.issue_key`, `sync.jira.synced_at`
- Issue type used: **Feature** (project had no "Story" type — Turkish locale)

### Step 3: Updated Story and Re-Synced (UPDATE)
- Added AC4: "Remember Me Functionality" to the markdown file
- Used `mcp_com_atlassian_editJiraIssue` to update existing issue `YI-4`
- Jira description now shows all 4 acceptance criteria
- `synced_at` timestamp updated in frontmatter
- **Note:** Got `MPC -32601: Method not found` error in UI, but verification confirmed the update went through successfully

## Key Concepts Learned

### CREATE vs UPDATE Logic
| Condition | Action |
|-----------|--------|
| No `sync.jira` in frontmatter | CREATE new issue |
| Has `sync.jira.issue_key` | UPDATE existing issue |

### Frontmatter as Sync State Tracker
```yaml
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-4"
    issue_key: "YI-4"
    synced_at: "2026-05-11T17:25:29Z"
```

### One-Way Sync
- **Direction:** Local markdown → Jira (one-way)
- **Source of truth:** Markdown files
- **Jira:** Acts as a mirror/view of the markdown content

## Files Created/Modified

| File | Action |
|------|--------|
| `specs/stories/STORY-001.md` | Created, then updated with AC4 and sync metadata |

## Jira Issue Details

| Field | Value |
|-------|-------|
| Issue Key | `YI-4` |
| Type | Feature |
| Summary | User Login Form |
| Status | Yapılacaklar (To Do) |
| Priority | Medium |
| Project | MCP Workshop (YI) |
| URL | https://yunusinal-workshop.atlassian.net/browse/YI-4 |

## Tools Used

| Tool | Purpose |
|------|---------|
| `getAccessibleAtlassianResources` | Discover cloud ID |
| `getVisibleJiraProjects` | List available projects & issue types |
| `createJiraIssue` | Create new Jira issue from markdown |
| `getJiraIssue` | Verify created/updated issue |
| `editJiraIssue` | Update existing issue with new content |
