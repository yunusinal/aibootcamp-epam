# Lab 01 — Context7: Up-to-Date Library Documentation

## Overview

This lab demonstrates how **Context7 MCP** solves the "outdated training data" problem by fetching **live, version-specific documentation** from official library sources instead of relying on an LLM's training data cutoff.

## Problem Statement

LLMs are trained on data up to a specific date. When libraries release new versions (e.g., React 19, Next.js 15), the model may:
- Return outdated syntax from older versions
- Hallucinate APIs that don't exist
- Provide no source attribution or version confirmation

**You can't verify whether the answer is correct.**

## Solution: Context7 MCP

Context7 is an MCP (Model Context Protocol) server that fetches live documentation from official sources in real-time.

### How It Works

```
Your Question → Context7 MCP Server → Identifies Library + Version
                                     → Fetches from Official Docs
                                     → Returns Content with Source URLs
                                     → LLM Uses This to Answer
```

### Two-Step MCP Tool Flow

| Step | Tool | Purpose |
|------|------|---------|
| 1 | `resolve-library-id` | Resolves a library name (e.g., "react") to a Context7-compatible ID (e.g., `/reactjs/react.dev`) |
| 2 | `get-library-docs` | Fetches up-to-date documentation for a specific topic from that library |

## Lab Results

### Without Context7 (Base Model Only)

| Aspect | Result |
|--------|--------|
| Source URL | ❌ None provided |
| Version confirmed | ❌ No |
| Accuracy | ⚠️ Unknown — could be hallucinated |
| Verifiability | ❌ Cannot verify |

### With Context7

| Aspect | Result |
|--------|--------|
| Source URL | ✅ GitHub URLs from official repos |
| Version confirmed | ✅ Pulled from latest official docs |
| Accuracy | ✅ Matches official documentation |
| Verifiability | ✅ Click source links to verify |

### Libraries Tested

#### 1. React — `use` Hook
- **Library ID:** `/reactjs/react.dev`
- **Source:** Official React documentation (react.dev)
- **Key finding:** The `use` hook can be called conditionally inside `if` statements and `for` loops — unique among React hooks
- **Code snippets returned:** 10 examples covering data fetching, context reading, and Suspense integration

#### 2. Next.js — Server Actions
- **Library ID:** `/vercel/next.js`
- **Source:** Official Vercel Next.js repository (canary branch)
- **Key finding:** Server Actions are enabled by default in Next.js 14+; use `'use server'` directive inside functions
- **Code snippets returned:** Multiple examples with form handling and auth checks

#### 3. Vue — Composition API `ref`
- **Library ID:** `/vuejs/vue`
- **Source:** Official Vue.js repository
- **Key finding:** Composition API uses `reactive`, `computed`, `watchEffect`, `onMounted`/`onUnmounted`
- **Code snippets returned:** Full TodoMVC example using Composition API

## When to Use Context7

| Scenario | Use Context7? |     Why |
|----------|---------------|---------|
| Fast-moving libraries (React, Next.js, Vue) | ✅ Yes |APIs change frequently between versions
| Version-specific documentation needed | ✅ Yes |Training data may have wrong version
| Verifying syntax against official docs | ✅ Yes |Eliminates hallucination risk
| Unsure if AI knowledge is current | ✅ Yes | Gets live data, not cached training
| Stable, unchanging APIs (basic JavaScript) | ❌ No | These rarely change
| General programming concepts | ❌ No | Concepts don't have "versions"
| Questions about your own codebase | ❌ No |Context7 fetches library docs, not your code

## MCP Configuration

Context7 is configured in `.vscode/mcp.json`:

```json
{
  "servers": {
    "io.github.upstash/context7": {
      "type": "stdio",
      "command": "npx",
      "args": ["@upstash/context7-mcp@1.0.31"],
      "env": {
        "CONTEXT7_API_KEY": "${input:CONTEXT7_API_KEY}"
      }
    }
  }
}
```

## Key Takeaway

> **Context7 eliminates the "works in docs but not in code" problem by fetching live documentation instead of relying on potentially outdated training data.**

## Next Lab

Proceed to [Lab 02 — Playwright MCP](lab-02-playwright.md) for browser automation testing.
