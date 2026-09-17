# WAR ROOM

**Data. Diagnosis. Decision. Consequence.**

WAR ROOM is a single-file, interactive business decision intelligence simulator. You play a Strategy & Analytics Manager investigating a company in crisis: revenue and customers are both growing, but profit is falling. You have to dig through synthetic-but-realistic Finance, Customer, Product, Pricing, Marketing and Operations data, form and test hypotheses, find the real root cause, make a call, defend it in front of the CEO/CFO/COO, and live with the simulated consequences.

This is not a dashboard with a game bolted on — the interface exists to serve the decision-making loop:

```
Signal → Investigation → Diagnosis → Decision → Defense → Consequence → Learning
```

## Try it

It's a single self-contained HTML file. No build step, no server, no dependencies to install.

- **Open it directly**: double-click `index.html`, or open it in a browser via `file://`.
- **Or serve it locally**:
  ```bash
  python3 -m http.server 8000
  # then visit http://localhost:8000
  ```
- **Or deploy with GitHub Pages** (recommended for sharing a link):
  1. Push this repo to GitHub.
  2. Go to **Settings → Pages**.
  3. Under "Build and deployment," set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`.
  4. Your app will be live at `https://<your-username>.github.io/<repo-name>/`.

## What's inside

- **A synthetic enterprise dataset**, generated deterministically (seeded PRNG) at page load: ~220 customers, several thousand transactions, products, marketing campaigns, and 24 months of finance rollups. Every number shown in the UI — KPIs, charts, hypothesis evidence, root-cause figures, decision impacts — is computed from this dataset at runtime, not hard-coded.
- **Case 001 — Profitability Under Pressure**, fully playable end to end:
  - Executive Dashboard with auto-surfaced "What Changed?" signals
  - Investigation Desk (Finance / Customers / Products / Pricing / Marketing / Operations tabs, with live charts via Chart.js)
  - Ask The Data — a natural-language query interface over the real dataset
  - Hypothesis Board — 5 hypotheses (including a marketing-CAC red herring), each with evidence for/against and a confidence estimate
  - Root-Cause Analysis — a causal evidence chain
  - Decision Center — 5 strategic options with modeled trade-offs
  - What-If Simulator — live sliders (discount, price, churn, marketing spend) vs. base case
  - The Boardroom — CEO / CFO / COO challenge your decision; your written responses are heuristically scored
  - Analyst Score — 7 categories (Problem Framing, Data Literacy, Root-Cause Reasoning, Financial Thinking, Strategic Thinking, Risk Awareness, Communication)
  - Consequence Engine — 30/90/365-day simulated outcomes based on your decision
  - Case Debrief and an Analyst Portfolio
- Navigation is locked in sequence — each phase unlocks as you complete the one before it, so you can't skip straight to the Decision Center without investigating first. Locked phases show a 🔒 in the sidebar and a tooltip explaining why.
- Cases 002–005 are previewed on the landing screen as "coming next" — only Case 001 is fully built out for now.

## Tech notes

- Zero build tooling: plain HTML/CSS/JS in one file (`index.html`).
- Charts via [Chart.js](https://www.chartjs.org/) (loaded from a CDN — needs internet access the first time it loads).
- Fonts: IBM Plex Sans / IBM Plex Mono via Google Fonts CDN.
- Portfolio persistence uses `window.storage`, an API provided by the Claude.ai artifact runtime. **Outside of Claude.ai** (e.g. plain GitHub Pages or opening the file locally), `window.storage` won't exist, so "Save to Portfolio" and the Portfolio screen will show a friendly fallback message instead of persisting — everything else in the app works the same either way. If you want real persistence outside Claude.ai, swap the calls in the `bindDebrief` / `bindPortfolio` functions for `localStorage` or a small backend.

## License

MIT — do whatever you'd like with it.
