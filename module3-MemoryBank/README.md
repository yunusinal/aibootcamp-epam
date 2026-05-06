# Module 03 — Context Engineering with Memory Banks (Cheat Sheet)

A personal summary of the EPAM **Context Engineering with Memory Banks** session and the hands-on lab in this repo.

- **Module focus:** Teaching AI assistants about YOUR project
- **Key question:** How do we give AI persistent, project-specific knowledge?
- **Practical outcome:** Configure memory banks that improve AI accuracy by **40–60%**

---

## The Journey So Far

| Module | Theme | Concept |
|---|---|---|
| 01 | Precision | Vibe coding fails, specs succeed |
| 02 | Structure | PRD → Epic → Story → Agents.MD ([specs/](specs/), [agents.md](agents.md)) |
| **03** | **Context** | **Teaching AI about YOUR project** ← this module |

---

## Part 1 — The Context Problem

**The problem:** AI coding assistants are **stateless by default** — every session starts fresh. Ask for a microservices endpoint Monday → AI follows your architecture. Ask Tuesday → AI uses a *different* architecture. AI doesn't remember previous conversations.

**Why it's expensive:**

| Model | Context window | Cost (input) |
|---|---|---|
| GPT-4 Turbo | 128K tokens | ~$10 / 1M |
| Claude Sonnet 4.5 | 200K tokens | ~$3 / 1M |
| Gemini Pro | 1M tokens | ~$1.25 / 1M |

A real codebase = 500K+ tokens — won't fit in one conversation. The challenge: **what to include, what to omit, how to organize for retrieval.**

**Without context — the auth middleware example:** AI generated generic Express + JWT code, but the team uses OAuth2, a standardized error format, required logging, and a shared auth client. **All wrong.**

**With context:** AI imports `OAuth2Client`, uses `ErrorResponse`, logs via the team logger, uses TypeScript types — all aligned with team standards.

**Cost of doing nothing (10-dev team):**
- 20 min/day × 20 days × 10 devs = **67 hrs/month** wasted
- @ $100/hr = **$6,700/month** = **$80,400/year** in context overhead
- With memory banks: 2–4 hr setup, 1–2 hr/month maintenance, **ROI positive in week 1**

---

## Part 2 — Memory Bank Fundamentals

**Definition:** Context engineering = systematic **design and management of context** provided to AI to improve output quality, consistency, and relevance.

**Three pillars:**
1. **Structure** — hierarchical, modular, versioned
2. **Content** — architecture, conventions, domain, history
3. **Delivery** — persistent, on-demand, progressive

### Memory Banks
**Structured knowledge repositories** that give AI persistent, project-specific context across sessions.

| Feature | Description |
|---|---|
| Persistent | Survives across sessions (unlike chat history) |
| Structured | Modular, hierarchical |
| Selective | Only relevant context per task |
| Versioned | Tracked as project evolves |
| Role-aware | Different context for Dev / QA / PM |

> Think of memory banks as: a **project handbook**, an **onboarding guide for a new AI teammate**, and **institutional knowledge encoded for machines**.

### Four Types of AI Memory

| Type | What | Example |
|---|---|---|
| **Episodic** | Specific past interactions | "Last time we discussed OAuth2" |
| **Semantic** ⭐ | General project knowledge | "Uses microservices + PostgreSQL" |
| **Procedural** ⭐ | "How to" workflows | "Adding API: schema → controller → tests" |
| **Working** | Current task (temporary) | "Working on Epic 2, Story 2.3" |

**Our focus:** Semantic + Procedural (most impactful for teams).

### Recommended Structure (matches [memory-banks/](memory-banks/))

```
memory-banks/
├── README.md          # Index and navigation
├── architecture/      # System design, ADRs, diagrams
├── conventions/       # From Agents.MD — coding/testing/naming/errors
├── domain/            # Glossary, business rules, personas (from PRD)
├── workflows/         # Dev process, code review, deployment
└── roles/             # developer.md, qa.md, pm.md
```

### Content Goldilocks

✅ **DO include:** architecture decisions, tech stack + versions, coding conventions, domain glossary, workflows, known issues, integration points
❌ **DON'T include:** secrets/credentials, PII, entire codebase, generated docs, overly detailed implementation, outdated info

> Too little → generic outputs · Too much → cognitive overload + cost · **Just right → accurate, efficient, cost-effective**

---

## Part 3 — The Context Engineering Stack

Three permanent layers + one temporary layer:

| Layer | Provides | Persistence | Example |
|---|---|---|---|
| **Memory Banks** | Project knowledge ("the world") | Permanent | "We use microservices with PostgreSQL" |
| **Agents.MD** | Coding rules ("the how") | Permanent | "TypeScript strict mode, 80% coverage" |
| **Skills** | Reusable workflows ("the actions") | Permanent | `/review-pr` — structured code review |
| **Inline Prompts** | Task details ("the what") | Temporary | "Implement login endpoint for Story 2.3" |

> **Key insight:** Without skills you re-explain workflows. Without memory banks you re-explain context. Without Agents.MD you re-explain conventions. **Context engineering eliminates repetition.**

### Skills (new concept this module)

Reusable, parameterized, shareable, composable prompt templates committed to the repo. Think **macros / runbooks / recipes** invoked via slash commands.

Example skill categories:
- **Specification:** `/create-prd`, `/decompose-story`, `/create-adr`
- **Development:** `/generate-tests`, `/implement-story`, `/refactor`
- **Quality:** `/review-pr`, `/security-check`, `/check-coverage`
- **Knowledge:** `/update-memory`

**Goldilocks rule:** A good skill is **20–60 lines** — enough structure for consistency, enough flexibility for adaptation.


---

## Verified Impact Data (from the deck)

**The context overhead problem (Industry research 2024–25):**
- 15–30 min/day per developer re-explaining context
- 32% of developer time wasted reconstructing lost context
- 41% more bugs in AI code lacking system context

**Verified gains:**
- **Anthropic Prompt Caching (2024):** 85% latency reduction · 90% cost reduction · ROI positive after 2 cached calls
- **GitHub Copilot Optimization (2024):** 20–35% cycle time reduction · 55% faster task completion · acceptance rates 20% → 35%



## Anti-Patterns to Avoid

| # | Mistake | Fix |
|---|---|---|
| 1 | The "everything file" — single 10K-line `memory.md` | Modular files (architecture / conventions / domain) |
| 2 | Code duplication — copying modules into memory | High-level patterns, link to source |
| 3 | Outdated info ("we use MongoDB" 6 months later) | Quarterly review, version control |
| 4 | Secrets in memory ("API key: abc123") | Never store secrets, use env vars |
| 5 | Over-prescription ("use exactly this algorithm…") | Provide principles + constraints, let AI implement |

---

## The Hands-On Lab (this repo)

**Goal:** Build memory banks for a real project and prove they improve AI output.

| Phase | Activity | Time |
|---|---|---|
| 1 | Create memory bank structure | 15 min |
| 2 | Write architecture overview | 20 min |
| 3 | Write conventions + domain glossary | 25 min |
| 4 | Write workflow documentation | 15 min |
| 5 | Test AI outputs (with/without memory) | 15 min |
| 6 | Peer review and refinement | 20 min |


### What I Built — [memory-banks/](memory-banks/)

| File | Purpose |
|---|---|
| [README.md](memory-banks/README.md) | Navigation index |
| [architecture/overview.md](memory-banks/architecture/overview.md) | System design, tech stack, deployment |
| [conventions/coding-standards.md](memory-banks/conventions/coding-standards.md) | Naming, testing, accessibility, error handling |
| [domain/glossary.md](memory-banks/domain/glossary.md) | Task, Column, Board terminology + business rules |
| [workflows/development-process.md](memory-banks/workflows/development-process.md) | Branch / PR / test / deploy process |

### Before / After Experiment

Same prompt, run twice — once without memory banks, once with. 
- Full breakdown: [memory-bank-impact.md](memory-bank-impact.md). 
- Raw outputs: [output-without-memory.md](output-without-memory.md)  . [output-with-memory.md](output-with-memory.md).

| Metric | Without | With | Δ |
|---|---|---|---|
| Files generated | 2 (`.jsx`, global CSS) | 4 (`.tsx` + CSS Module + types + tests) | Correct structure |
| TypeScript compliance | 0% | 100% | Full |
| Acceptance criteria met | 1/5 | 4/5 | +3 |
| Issues to fix | 12 | 1 | **−92%** |
| Test coverage | 0 tests | 8 tests | From zero |
| Accessibility | None | WCAG 2.1 AA | Full |
| Correction time | 25–35 min | 3–5 min | **~85% saved** |

**Biggest impact files:** 
-  `conventions/coding-standards.md` (file types, naming, tests, a11y) and 
- `domain/glossary.md` (data model, `crypto.randomUUID()`, `ColumnType`, validation rules).

---

## What I Learned

1. **Context engineering ≠ prompt engineering.** Prompts are transient; memory banks are persistent, versioned context.
2. **AI is stateless by default** — every session forgets. Memory banks make it remember.
3. **The stack matters:** Memory Banks (world) + Agents.MD (how) + Skills (actions) + Prompts (what) = high-quality output.
4. **Specificity beats volume.** Versions, exact naming patterns, and concrete examples beat long prose.
5. **Semantic + Procedural memory** are the highest-leverage types for engineering teams.
6. **Start simple:** 4–5 files, 5–10 pages, then iterate based on AI output quality.
7. **Test the impact.** A before/after run quantifies value and exposes gaps.
8. **Maintenance is cheap (1–2 hr/month) vs. the cost of doing nothing ($80K+/year per 10-dev team).**

---

## Quick File Index


- SDD agent rules → [agents.md](agents.md)
- Specs (PRD, epics, stories) → [specs/](specs/)
- Memory banks → [memory-banks/](memory-banks/)
- Impact analysis → [memory-bank-impact.md](memory-bank-impact.md)
- AI output (no memory) → [output-without-memory.md](output-without-memory.md)
- AI output (with memory) → [output-with-memory.md](output-with-memory.md)

---

## TL;DR

> Memory Banks turn an AI assistant from a generic code generator into a **project-aware teammate**. The full **Context Engineering Stack** (Memory Banks + Agents.MD + Skills + Inline Prompts) eliminates the **15–30 min/day** every developer wastes re-explaining context — saving and improving AI accuracy **40–60%**. In my own test: **92% fewer issues, ~85% less correction time.**

