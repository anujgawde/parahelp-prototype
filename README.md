# Parahelp UI

Operator command center for [Parahelp](https://parahelp.com)'s AI support agents — act on configs, tests, and tickets inline.

> The operator should not just approve the agent's plan. The operator should be able to steer it.

## What's Built

### Actionable Dashboard (`/dashboard`)

A Gmail AI Inbox-style summary replacing traditional analytics charts. Operators see what happened and what needs their attention.

- **Agent summary** with animated stat counters (configs, tests, published, gaps)
- **Action cards** operators can act on directly:
  - Approve & publish a config inline
  - Run tests in real-time with progress bar and individual results
  - Review & refine an agent's resolution plan (links to HITL flow)
  - View blocked gaps with expandable detail
  - Acknowledge and dismiss items
- **Weekly summary** with expandable topic rows and progress rings

### Human-in-the-Loop with Editable Reasoning (`/tickets/[id]`)

When a ticket needs operator review, the agent's plan is fully editable before execution.

- **Editable resolution plan** — inline text editing, toggle steps on/off, reorder, add/remove steps
- **Context source control** — add or remove knowledge sources that feed the plan
- **Simulation panel** — side-by-side comparison of original vs modified plan metrics (confidence, risk, success rate) with explanations
- **Execution decision** — select which plan to execute, confirm with a loader, see success confirmation

### Guided Tour

A walkthrough that connects both flows. Auto-starts on first visit, replayable via the "Start tour" button on the dashboard.

**Dashboard (4 steps):**
1. Agent summary overview
2. Key metrics
3. Publish a config (user clicks "Approve & publish")
4. HITL review (user clicks "Review & refine plan")

**Ticket page (5 steps):**
1. Support issue received
2. Agent retrieves context
3. Refine the plan
4. Simulate outcome
5. Execute

### Other Pages

- `/tests` — Agent testing with real-time test execution and publish flow
- `/tickets` — Ticket list with status indicators
- `/scheduled` — Scheduled automation tasks
- `/controls` — Agent configuration (thresholds, escalation rules, aggressiveness)
- `/` — Chat / assistant conversations

## Tech Stack

- **Framework:** Next.js 16 (App Router, Turbopack)
- **Language:** TypeScript
- **Styling:** Tailwind CSS v4
- **Animations:** NumberFlow (stat counters), CSS animations (fade, slide, guide)
- **Charts:** Recharts
- **Analytics:** Vercel Analytics
- **No external UI component libraries** — all components built from scratch

## Getting Started

```bash
npm install
npm run dev
```

Open [http://localhost:3000/dashboard](http://localhost:3000/dashboard) to start the guided tour.

## Project Structure

```
src/
├── app/
│   ├── dashboard/       # Actionable dashboard
│   ├── tickets/         # Ticket list + detail with HITL
│   ├── tests/           # Agent testing with real-time execution
│   ├── scheduled/       # Scheduled automations
│   ├── controls/        # Agent configuration
│   └── page.tsx         # Chat / conversations
├── components/
│   ├── guided/          # Tour system + HITL components
│   ├── layout/          # AppShell, Sidebar
│   ├── ticket/          # Ticket card, agent reasoning
│   ├── chat/            # Chat input, messages, actions
│   ├── testing/         # Memory file + test case cards
│   ├── ui/              # Panel, Slider, Toggle, etc.
│   └── icons/           # SVG icon components
└── data/                # Mock data (tickets, configs, tests)
```

## Design Decisions

- **Near-black accent color** — only status/sentiment chips use color (green, orange, red)
- **Sidebar background:** `rgb(248, 247, 246)` matching Parahelp's existing style
- **No charts on dashboard** — the dashboard emphasizes actionable items over passive analytics
- **Persistent tour state** — survives page navigation via localStorage
- **Cards expand on hover** — action buttons appear without reserving vertical space at rest
