# Lab 02 — Playwright: AI-Driven Browser Automation

## Overview

This lab demonstrates how **Playwright MCP** enables browser automation through **natural language** — no code, no selectors, no scripts required. The AI translates your plain-English instructions into Playwright browser actions automatically.

## Problem Statement

Traditional browser automation requires:
- Learning the Playwright API
- Writing CSS/XPath selectors manually
- Managing page objects and test fixtures
- Debugging flaky selectors when the UI changes

**Playwright MCP eliminates all of this for ad-hoc tasks.**

## How Playwright MCP Works

```
Your Natural Language Request
    → browser_navigate (opens URL)
    → browser_snapshot (reads accessibility tree)
    → browser_fill_form / browser_type (fills inputs)
    → browser_click (clicks buttons/links)
    → browser_take_screenshot (captures result)
```

The AI uses the **accessibility tree** (not CSS selectors) to identify page elements. Each element gets a ref (e.g., `e16` for username textbox) that the AI resolves automatically from your description.

## Lab Results

### Step 1: Navigate & Screenshot

- **URL:** `https://example.com`
- **Tools invoked:** `browser_navigate` → `browser_take_screenshot`
- **Output:** Full-page PNG screenshot saved as `lab02-example-com.png`
- **Accessibility snapshot:** Showed h1 heading "Example Domain", a paragraph, and a "Learn more" link — all detected without selectors

### Step 2: Automated Login Form

- **URL:** `https://the-internet.herokuapp.com/login`
- **Tools invoked (5-step flow):**

| Step | MCP Tool | Action |
|------|----------|--------|
| 1 | `browser_navigate` | Opened the login page |
| 2 | `browser_snapshot` | Read accessibility tree — found Username textbox, Password textbox, Login button |
| 3 | `browser_fill_form` | Filled "tomsmith" into username, "SuperSecretPassword!" into password |
| 4 | `browser_click` | Clicked the Login button |
| 5 | `browser_take_screenshot` | Captured the success page |

- **Result:** Page navigated to `/secure` with message **"You logged into a secure area!"**
- **Screenshot:** Saved as `lab02-login-success.png`

### Key Observation

The AI generated this Playwright code automatically behind the scenes:
```js
await page.getByRole('textbox', { name: 'Username' }).fill('tomsmith');
await page.getByRole('textbox', { name: 'Password' }).fill('SuperSecretPassword!');
await page.getByRole('button', { name: ' Login' }).click();
```
We never wrote any of this — it was derived from the accessibility tree snapshot.

## Practical Use Cases

| Use Case | Example | Benefit |
|----------|---------|---------|
| **E2E Testing** | "Test the registration flow end-to-end" | Automated smoke tests without code |
| **UX Review** | "Explore the site and report confusing elements" | AI identifies friction points |
| **Screenshot Documentation** | "Capture each checkout step with screenshots" | Auto-generated visual guides |
| **Regression Testing** | "Verify login still works after deployment" | Quick post-deploy verification |

## Playwright MCP vs Playwright Library

| Aspect | Playwright MCP | Playwright Library |
|--------|----------------|-------------------|
| **Input** | Natural language prompts | JavaScript/TypeScript/Python code |
| **Selectors** | Auto-detected via accessibility tree | Manual CSS/XPath/role selectors |
| **Best for** | Ad-hoc testing, exploration, prototyping | Production test suites, CI/CD |
| **Repeatability** | Prompt-based (may vary) | Code-based (deterministic) |
| **Learning curve** | None | Must learn Playwright API |
| **When to choose** | Quick checks, one-off tasks | Serious test automation at scale |

## MCP Configuration

Playwright MCP is configured in `.vscode/mcp.json`:

```json
{
  "servers": {
    "microsoft/playwright-mcp": {
      "type": "stdio",
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

## Screenshots

- `lab02-example-com.png` — Example.com homepage
- `lab02-login-success.png` — Successful login result page

## Key Takeaway

> **Playwright MCP translates natural language into browser automation, using the accessibility tree to identify elements — no selectors, no code, no manual effort.**

## Next Lab

Proceed to [Lab 03 — Jira Sync](lab-03-jira-sync.md) for Atlassian integration.
