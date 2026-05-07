# Module 04 — MCP & Skills (Cheat Sheet)

A personal summary of the EPAM **MCP & Skills** session (Feb 2026 deck) and the five hands-on labs in this repo.

- **Module focus:** Connecting AI assistants to external tools and data with **MCP**, then layering **Skills** on top for domain expertise
- **Key question:** How do we extend AI capabilities **beyond chat**?
- **Practical outcome:** Working sync workflows for Jira, Confluence, and dev tools — plus a mental model for when to reach for **MCP** vs **Skills**

## Module Learning Objectives (from the deck)

1. Explain **what MCP is and why it matters**
2. **Configure MCP servers** in GitHub Copilot
3. Use **Context7** for up-to-date library documentation
4. Use **Playwright** for browser automation
5. **Sync local markdown specs** to Jira and Confluence
6. **Create reusable sync prompts** with out-of-date detection

---

## The Journey So Far

| Module | Theme | Concept |
|---|---|---|
| 01 | Precision | Vibe coding fails, specs succeed |
| 02 | Structure | PRD → Epic → Story → Agents.MD |
| 03 | Context | Memory Banks — teaching AI about YOUR project |
| **04** | **Tools** | **MCP — giving AI hands, eyes, and live data** ← this module |

---

## Part 1 — The Tool Problem (and what MCP is)

**The problem:** Even a perfectly-prompted, memory-bank-equipped AI is still **trapped in the chat window**. It can:
- Talk *about* React 19 but not *read* the latest React 19 docs
- Describe a login test but not *click the button*
- Reference Jira issue YI-4 but not *create or update it*
- Reference Confluence page 655361 but not *publish to it*

Without tools, every action requires a human in the loop — copy/paste, screenshot, manual update, manual sync.

**MCP (Model Context Protocol)** is the open standard that lets an AI assistant **call external tools** through a uniform interface — fetch live data, drive browsers, hit APIs, mutate state — all from natural language inside Copilot Chat.


> **Key takeaway from the deck:** *MCP is no longer emerging — it is the industry standard for AI tool integration. Skills you learn today work across all major platforms* (Anthropic, OpenAI, Google DeepMind, Microsoft, Cursor, Zed, Sourcegraph, Replit, …).

### How MCP Works — Architecture

**Client–Server model with three roles:**

| Role | Examples | Purpose |
|---|---|---|
| **Host** | Claude, VS Code, Cursor, your code | Owns the conversation |
| **MCP Client** | Built into the host | Connects to servers via the protocol |
| **MCP Server** | Context7, Playwright, Atlassian, … | Exposes capabilities |

**What servers expose:**
- **Tools** — actions the AI can perform (create issue, take screenshot)
- **Resources** — data the AI can read (docs, DB schemas)
- **Prompts** — pre-defined templates for common operations

```
Natural language
   ↓
Copilot decides which MCP tool to call
   ↓
MCP server executes (Context7 / Playwright / Atlassian / …)
   ↓
Structured result back to the model
   ↓
Model answers, edits files, or chains the next call
```

Every server is configured once in `.vscode/mcp.json` and exposes a set of tools. The model picks the right tool from your prompt.

### Where MCP Is Used in Practice (from the deck)

| Domain | Example |
|---|---|
| **AI-assisted coding** | Copilot, Cursor, Replit, Sourcegraph, Codeium — **40–60% faster agent deployment** |
| **Agentic / multi-agent** | LangChain, AutoGen, CrewAI use MCP as the standard tool interface |
| **Retail** | One AI conversation: check inventory → process refund → update loyalty |
| **Telecom** | AI diagnoses outage → schedules technician → notifies customer |
| **DevOps** | AI monitors OpenShift → detects anomalies → posts to Slack via MCP |
| **Forecast** | Gartner: by **2028, 33% of enterprise apps** will embed agentic AI |

---

## Part 2 — The Five Labs at a Glance

| # | Lab | MCP Server | What it gives the AI |
|---|-----|-----------|----------------------|
| 01 | [Context7](lab01-context7-README.md) | `@upstash/context7-mcp` | **Live, version-specific library docs** (React 19, Next.js 15, Vue) |
| 02 | [Playwright](lab02-playwright-README.md) | `@playwright/mcp` | **Browser control via accessibility tree** — no selectors |
| 03 | [Jira Sync](lab03-jira-sync-README.md) | `com.atlassian/atlassian-mcp-server` | **Create / update Jira issues** from markdown |
| 04 | [Confluence Sync](lab04-confluence-sync-README.md) | `com.atlassian/atlassian-mcp-server` | **Publish / update Confluence pages** from markdown |
| 05 | [Reusable Prompts](lab05-reusable-prompts-README.md) | (uses 03 + 04) | **Team-shared `/slash-command` workflows** for batch sync |

---

## Part 3 — Lab Deep Dives

### Lab 01 — Context7: Up-to-Date Library Docs

**Problem:** LLM training data is frozen. Ask about React 19 or Next.js 15 → outdated syntax, hallucinated APIs, no source attribution. **You can't verify the answer.**

**Solution:** Two-step MCP flow that fetches live docs from the official source.

| Step | Tool | Purpose |
|---|---|---|
| 1 | `resolve-library-id` | "react" → `/reactjs/react.dev` |
| 2 | `get-library-docs` | Pulls topic-scoped docs + GitHub source URLs |

**Verified results:**

| Aspect | Without Context7 | With Context7 |
|---|---|---|
| Source URL | ❌ None | ✅ Official GitHub URLs |
| Version confirmed | ❌ No | ✅ Latest official |
| Verifiability | ❌ Cannot verify | ✅ Click to verify |

**Libraries tested:** React (`use` hook can be called conditionally — unique among hooks), Next.js (Server Actions, `'use server'`), Vue (Composition API TodoMVC).

**Use it when:** fast-moving libraries, version-specific syntax, anti-hallucination checks.
**Skip it when:** stable APIs, language fundamentals, your own codebase.

### Lab 02 — Playwright: AI-Driven Browser Automation

**Problem:** Traditional browser automation = learn the API, hand-write CSS/XPath selectors, maintain page objects, debug flaky tests when UI changes.

**Solution:** Natural-language → browser actions via the **accessibility tree** (not selectors).


**Lab evidence:** 5-step automated login on `the-internet.herokuapp.com/login` — page reached `/secure` with "You logged into a secure area!" — captured in [lab02-login-success.png](lab02-login-success.png). The AI internally generated `getByRole('textbox', { name: 'Username' }).fill('tomsmith')` etc. — **we never wrote a line of Playwright code**.

**MCP vs library:**

| | Playwright MCP | Playwright Library |
|---|---|---|
| Input | Natural language | TS/JS/Python code |
| Selectors | Auto, via a11y tree | Manual CSS/XPath |
| Best for | Ad-hoc, exploration, smoke checks | Production CI test suites |
| Repeatability | Prompt-based | Deterministic |

### Lab 03 — Jira Sync (Atlassian MCP)

Synced [specs/stories/STORY-001.md](specs/stories/STORY-001.md) → Jira issue **YI-4** in project `YI` (`MCP Workshop`).

**The CREATE / UPDATE pattern** — driven entirely by frontmatter:

| Frontmatter | Action |
|---|---|
| No `sync.jira` block | `createJiraIssue` |
| Has `sync.jira.issue_key` | `editJiraIssue` |

**Sync state lives in the markdown:**
```yaml
sync:
  jira:
    url: "https://yunusinal-workshop.atlassian.net/browse/YI-4"
    issue_key: "YI-4"
    synced_at: "2026-05-11T17:25:29Z"
```

**Direction:** one-way, markdown → Jira. Markdown is the **source of truth**; Jira is a mirror.

**Real-world catch:** project had no "Story" issue type (Turkish-locale instance), so `Feature` was used — a reminder to call `getJiraProjectIssueTypesMetadata` before assuming a type exists.

### Lab 04 — Confluence Sync (Atlassian MCP)

Synced [specs/prds/PRD-001.md](specs/prds/PRD-001.md) → Confluence page **655361** in space **MCPDOCS**.

| Step | Action | Result |
|---|---|---|
| 1 | CREATE page from markdown | New `pageId 655361`, version 1 |
| 2 | Edit PRD locally (added FR-5) | — |
| 3 | UPDATE same page | Same `pageId`, **version bumped to 2** |

```yaml
sync:
  confluence:
    url: "…/spaces/MCPDOCS/pages/655361/User+Authentication+PRD"
    page_id: 655361
    space_key: MCPDOCS
    synced_at: "2026-05-11T16:10:39Z"
```

**Key learnings:**
- Atlassian MCP **converts markdown → Confluence storage HTML** automatically (headings, lists, tables preserved).
- Tracking `page_id` + `synced_at` makes re-syncs **idempotent**.
- CREATE = new pageId; UPDATE = same pageId + `version.number += 1`.

### Lab 05 — Reusable Sync Prompts

Wraps Labs 03–04 into team-shared, version-controlled `/slash-command` prompt files in `.github/prompts/`:

| Prompt | Purpose |
|---|---|
| `/sync-to-jira` | Batch sync `specs/stories/` to Jira (with epic parent links) |
| `/sync-to-confluence` | Batch sync `specs/prds/` to Confluence |
| `/check-sync-status` | Classify every spec file as NEW / OUT-OF-DATE / UP-TO-DATE / ORPHANED |
| `/sync-plan` | Two-way diff with conflict detection + approval gate |

**The five sync states:**

| State | Frontmatter | Remote | Action |
|---|---|---|---|
| 🆕 NEW | No `sync` block | — | CREATE |
| ⚠️ OUT-OF-DATE | `synced_at` < file mtime | Exists | UPDATE |
| ✅ UP-TO-DATE | `synced_at` ≥ file mtime | Exists | Skip |
| ❌ ORPHANED | Has `sync` | Deleted | Clean up |
| ⚠️ CONFLICT | Both sides changed | Exists | Merge |

Every prompt follows **Discover → Analyze → Preview → Approve → Execute → Report**. **Nothing pushes without confirmation.**

---

## Part 4 — Skills: The Knowledge Layer on Top of MCP

The deck spends as much time on **Skills** as on MCP. Skills aren't built in this lab pack yet, but they're the natural next step — and the mental model matters.

### MCP vs Skills — the core distinction

| | **MCP** | **Skills** |
|---|---|---|
| **What** | Protocol (connections) | Knowledge packages (workflows + reference docs) |
| **Provides** | Ability to **act** | Domain expertise + instructions on **how to act** |
| **Without it** | AI can't reach external tools | AI can reach tools but lacks domain knowledge |
| **Created by** | Server developers | **Your team**, stored in `.claude/skills/` |
| **Analogy** | **Roads & bridges** of a city | **Navigation system** with maps + traffic + local knowledge |

> **Rule of thumb:** MCP = raw capability. Skill = domain-expertise package that **uses** that capability.

### What a Skill is

> **Definition (from the deck):** Agent skills are **versioned knowledge packages** stored in `.claude/skills/` that bundle workflows, reference documentation, schemas, and scripts into self-contained domain expertise for AI coding assistants.

Five characteristics:

| Feature | Meaning |
|---|---|
| **Self-contained** | Everything the AI needs for a domain in one directory |
| **Rich** | `SKILL.md` + reference docs + schemas + scripts |
| **Versioned** | Lives in git, reviewed in PRs |
| **Shareable** | Whole team gets the same domain knowledge |
| **Composable** | Skills can call MCP tools and other resources |

### Skill Anatomy

```
.claude/skills/
└── <category>/
    └── <skill-name>/
        ├── SKILL.md          ← entry point (YAML frontmatter + decision tree)
        ├── reference-doc.md  ← domain docs
        ├── schemas/          ← format specs
        ├── scripts/          ← helper tools
        └── LICENSE.txt
```

`SKILL.md` frontmatter:
```yaml
---
name: docx
description: "Comprehensive document creation, editing, and analysis with support for tracked changes, comments, formatting preservation"
license: Proprietary
---
```

The body is a **decision tree**, not linear steps:
```markdown
## Workflow Decision Tree
### Reading/Analyzing Content   → use "Text extraction"
### Creating New Document       → use "Creating new Word document"
### Editing Existing Document
- Your own doc       → Basic OOXML editing
- Someone else's doc → Redlining workflow
- Legal/business     → Redlining (required)
```

**Skills are auto-discovered** — the AI loads the relevant `SKILL.md` when it matches the task description.

### Skills vs Commands — the evolution

| | **Commands** (`.claude/commands/`) | **Skills** (`.claude/skills/`) |
|---|---|---|
| Structure | Single `.md` file | Directory with `SKILL.md` + resources |
| Invocation | `/command-name` (explicit) | Auto-discovered by AI |
| Content | Step-by-step instructions | Decision trees + reference docs + schemas |
| Context | Only what's in the prompt | Full domain knowledge package |
| Best for | Simple, repeatable tasks | Complex domains needing expertise |

> A command is a **recipe card**. A skill is an expert's **complete reference library**.

### When to use MCP vs when to use Skills

**Use MCP** when you need AI to **act**: read/write Jira, automate browsers, query DBs, hit APIs.

**Use Skills** when you need AI to have **domain expertise**:

| Scenario | Skill | Why not just MCP? |
|---|---|---|
| Create professional `.docx` | `document-skills/docx/` | MCP can write files; skill knows OOXML schemas & formatting |
| Build presentations | `document-skills/slidev/` | MCP can't know slide layout rules / theme constraints |
| Apply format standards | `document-skills/pdf/` | Skill packages conversion logic + quality checks |
| Encode team conventions | Custom skill | MCP can't know your team's processes |

### Building Effective Skills

**SKILL.md best practices:**
- Clear `name`, `description`, `license` frontmatter (AI uses these to match tasks)
- **Decision tree, not linear steps** — branch by scenario
- Reference bundled docs (schemas, scripts) in the same directory
- Handle edge cases ("If format invalid, use redlining workflow")
- Keep `SKILL.md` focused on workflow logic — push details into reference docs

**Quality test (4 questions):**
1. Does the AI auto-discover it for the right tasks?
2. Are reference materials sufficient for correct output?
3. Does the decision tree cover all common scenarios?
4. Can a new team member understand the skill structure?

**Skill evolution pattern:** Ad-hoc explanations → `/command` → full skill → mature skill (with schemas/scripts) → shared skill (reviewed in PRs).

---

## Part 5 — Cross-Cutting Patterns

### 1. Frontmatter as Sync State
The same idea powers Jira *and* Confluence *and* the batch prompts: a tiny YAML block in the markdown is the **single source of sync truth**. No separate database, no `.synced.json` sidecar.

### 2. Markdown is the Source of Truth
Every external system (Jira, Confluence) is treated as a **mirror**. One-way sync keeps mental model + tooling simple.

### 3. Discover → Preview → Approve → Execute
Destructive operations (CREATE/UPDATE/DELETE on shared systems) **always** show a plan first and wait for approval. Lab 05 codifies this; Labs 03–04 do it informally.

### 4. Accessibility-First Element Targeting
Playwright MCP picks elements by **role + accessible name**, not CSS. Side-effect: if the AI can find it, a screen-reader user can too.

### 5. Version-Pinned MCP Servers
`.vscode/mcp.json` pins exact versions (`@upstash/context7-mcp@1.0.31`, `atlassian-mcp-server v1.1.1`). MCP servers evolve fast — pinning prevents silent breakage.

---

## Part 6 — The Full Context Engineering Stack (now complete)

| Layer | Provides | Persistence | Module |
|---|---|---|---|
| **Memory Banks** | Project knowledge ("the world") | Permanent | 03 |
| **Agents.MD** | Coding rules ("the how") | Permanent | 02 |
| **Skills** | **Domain expertise packages** (decision trees + schemas + scripts) | Permanent | **04** |
| **Prompt Files / Commands** | Reusable simple workflows | Permanent | 03 + **04 (Lab 05)** |
| **MCP Servers** | **Live tools ("the hands & eyes")** | Permanent | **04** |
| **Inline Prompts** | Task details ("the what") | Temporary | every module |

> Memory banks taught the AI *about* the project. **MCP gave it hands.** **Skills give those hands expertise.**

---

## Anti-Patterns to Avoid

| # | Mistake | Fix |
|---|---|---|
| 1 | Calling Context7 for stable APIs (`Array.map`) | Save it for fast-moving libs (React 19, Next.js 15) |
| 2 | Using Playwright MCP as a CI test framework | Use it for exploration; use the real Playwright lib in CI |
| 3 | Two-way Jira/Confluence sync from day one | Start one-way (markdown → remote) |
| 4 | No `synced_at` / `page_id` tracking → duplicate issues | Always write sync state back to frontmatter |
| 5 | `/slash-command` that pushes without preview | Enforce Discover → Preview → Approve → Execute |
| 6 | Storing OAuth tokens in repo | OAuth lives in the MCP server / VS Code secrets, never in `.vscode/mcp.json` |
| 7 | Assuming "Story" issue type exists | Always call `getJiraProjectIssueTypesMetadata` first |
| 8 | Floating MCP server versions | Pin exact versions in `.vscode/mcp.json` |

---

## When to Reach for Which Tool

| If you need to… | Use |
|---|---|
| Quote the latest official API of a library | **Context7 (MCP)** |
| Click around a web app in plain English | **Playwright (MCP)** |
| Push a story from `specs/` into Jira | **Atlassian Jira (MCP)** |
| Publish a PRD into a Confluence space | **Atlassian Confluence (MCP)** |
| Run any of the above as a repeatable team flow | **Reusable prompt file / command** |
| Bundle deep domain expertise the team can share | **Skill** in `.claude/skills/` |

---

## What I Learned

1. **MCP closes the loop.** Memory + specs tell the AI *what* to do; MCP lets it *do* it. The deck's framing — *"USB for AI"* — finally clicked once I configured my second server.
2. **MCP is no longer emerging.** It's the industry standard (Anthropic, OpenAI, Google, Microsoft, 300+ clients, 10K+ servers). What you learn on one host transfers to all of them.
3. **MCP and Skills are different layers, not alternatives.** MCP = the road. Skill = the navigation system that knows where to drive.
4. **Frontmatter is a tiny but powerful database** — sync state, idempotency, and CREATE/UPDATE routing all fit in 5 lines of YAML.
5. **Live docs beat trained docs** every time for fast-moving libraries — Context7 turns "I think the API looks like…" into "here's the official source URL."
6. **Accessibility tree > CSS selectors** for AI-driven browsers. Less brittle, and a free a11y signal.
7. **One-way sync first.** Markdown → Jira / Confluence is simple, predictable, and never destroys upstream edits you didn't expect.
8. **Out-of-date detection compares content, not timestamps** (timestamps churn on assignee/status/comment updates too).
9. **Always Discover → Preview → Approve → Execute** for any tool that mutates shared systems.
10. **Pin MCP server versions** — these are young, evolving projects.
11. **A skill is a decision tree, not a checklist.** Branching on scenario is what makes it scale beyond a single-purpose command.

