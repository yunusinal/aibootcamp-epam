# Architecture Overview: module3-yi (Personal Task Board)

## System Architecture

### Pattern: Single-Page Application (SPA) — Client-Side Only

We use a purely client-side SPA with no backend services. This architecture supports:
- **Zero-setup experience** — no server deployment, no account creation, no database provisioning
- **100% offline functionality** — all features work without network connectivity after initial load
- **Instant load times** — static assets served from a single HTML entry point
- **Data privacy** — all user data stays in the browser, never leaves the device

### Key Components

```
┌─────────────────────────────────────────────────────┐
│                    Browser (Client)                   │
├─────────────────────────────────────────────────────┤
│  App Shell (App.tsx)                                 │
│  ├── Board Selector       → multi-board switching    │
│  ├── Board View           → renders columns + tasks  │
│  │   ├── Column (To Do)                             │
│  │   ├── Column (In Progress)                       │
│  │   └── Column (Done)                              │
│  ├── Task Card            → individual task display  │
│  ├── Task Form            → create/edit task inline  │
│  └── Keyboard Shortcut    → overlay help panel       │
├─────────────────────────────────────────────────────┤
│  Custom Hooks Layer                                  │
│  ├── useLocalStorage      → read/write persistence   │
│  ├── useDragAndDrop       → drag-and-drop logic      │
│  └── useKeyboardShortcuts → shortcut handling        │
├─────────────────────────────────────────────────────┤
│  localStorage (Browser API)                          │
│  └── JSON-serialized board/task data (≤ 5MB)         │
└─────────────────────────────────────────────────────┘
```

### Communication Patterns
- **No network communication** — the app makes zero external HTTP requests (no APIs, no CDNs at runtime, no analytics)
- **Component communication** — React props (parent → child) and callback functions (child → parent)
- **State persistence** — synchronous read/write to `localStorage` on every state change via custom `useLocalStorage` hook

### Data Flow
1. On app load: read JSON from `localStorage` → parse → hydrate React state
2. User action (create/edit/move/delete task) → update React state → serialize to JSON → write to `localStorage`
3. All operations are synchronous and atomic — no eventual consistency concerns

---

## Tech Stack

### Frontend
- **Framework:** React 18 (functional components, hooks only — no class components)
- **Build Tool:** Vite (latest stable)
- **Language:** TypeScript 5.x in strict mode (`"strict": true` in tsconfig)
- **Styling:** CSS Modules (`.module.css`) or plain CSS — no Tailwind, no MUI, no external UI libraries
- **State Management:** React useState/useReducer + custom hooks — no Redux, no Zustand, no external state libraries

### Persistence
- **Storage:** Browser `localStorage` API
- **Format:** JSON-serialized objects
- **Limits:** ≤ 5MB total, ≤ 100 tasks per board, ≤ 10 boards
- **No database, no IndexedDB, no backend API**

### Development Tools
- **Package Manager:** npm
- **Linting:** ESLint with TypeScript rules
- **Type Checking:** TypeScript compiler (`tsc --noEmit`)
- **Dev Server:** Vite dev server with HMR

### Testing (planned)
- **Unit Tests:** Vitest (Vite-native test runner)
- **Component Tests:** React Testing Library
- **Accessibility Audits:** axe-core

### Browser Targets
- **ES2020+** — last 2 versions of Chrome, Firefox, Safari, Edge
- **Viewport:** 768px–1920px (desktop only, no mobile optimization)

---

## Deployment

### Strategy: Static Site Deployment

Since the app is purely client-side with no backend, deployment consists of serving static files (HTML, JS, CSS).

### Build Process
1. `npm run build` → Vite produces optimized static assets in `dist/`
2. Output: single `index.html` + hashed JS/CSS bundles
3. No server-side rendering, no API routes, no environment variables at runtime

### Environments
- **dev:** `npm run dev` → Vite dev server with HMR on `localhost:5173`
- **production:** Static files served from any static host (GitHub Pages, Netlify, Vercel, or simple file server)

### CI/CD Pipeline (if applicable)
1. Push to GitHub triggers workflow
2. Install dependencies (`npm ci`)
3. Run linting (`npm run lint`)
4. Run type checking (`tsc --noEmit`)
5. Run tests (`npm test`)
6. Build production bundle (`npm run build`)
7. Deploy `dist/` to static hosting

### Rollback
- Revert to previous Git commit and re-deploy — static files make rollback trivial

---

## Key Architectural Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| No backend | localStorage only | Zero-setup, offline-first, data privacy, no hosting cost |
| React 18 | Functional components + hooks | Modern patterns, excellent ecosystem, developer familiarity |
| TypeScript strict | No `any` types allowed | Catch errors at compile time, self-documenting code |
| CSS Modules | No external UI lib | Small bundle size, full styling control, no dependency risk |
| Vite | Not CRA or webpack | Fast HMR, native ESM, minimal config, modern tooling |
| localStorage | Not IndexedDB | Simpler API, synchronous, sufficient for ≤ 5MB data |
| No state library | useState + custom hooks | App complexity doesn't warrant Redux/Zustand overhead |

---

## Performance Requirements

| Metric | Target | How to Verify |
|--------|--------|---------------|
| Initial render (50 tasks) | ≤ 500ms | Lighthouse performance audit |
| Drag-and-drop feedback | ≤ 100ms | Chrome DevTools Performance tab |
| localStorage read/write | ≤ 50ms | Performance.now() timing |
| Bundle size | Minimal (no heavy deps) | `npm run build` output analysis |

---

## Security Considerations

- **No network requests** — eliminates CSRF, SSRF, and data exfiltration risks
- **XSS prevention** — all user-provided text (task titles, descriptions) must be sanitized before rendering; React's JSX escaping handles most cases, but dangerouslySetInnerHTML is forbidden
- **No sensitive data** — localStorage stores only task/board data, no credentials or PII
- **Content Security Policy** — can restrict to `self` only since no external resources needed