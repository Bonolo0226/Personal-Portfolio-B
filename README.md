# Personal Finance AI Advisor 

A portfolio project for the Week 4 AI Bootcamp (Finance industry).
It analyses monthly spending, flags risks, and produces a personal
finance health score with plain-English recommendations.

> **Offline mode:** this version uses deterministic, rule-based logic
> instead of an external LLM API. No API key, no network calls — but
> the architecture and prompt chain are identical to the LLM version.

## Features

- 📊 Upload or paste a month of transactions (CSV) and get an instant analysis
- 🏷️ Auto-categorisation via transparent keyword rules (14 categories)
- ⚠️ Risk detection: housing burden, discretionary spending, low savings rate, subscription stacking
- 💯 0–100 financial health score with plain-English explanation
- ✅ Three personalised recommendations plus a "quick win"
- 🇿🇦 **Amounts displayed in South African Rand (R)** via `Intl.NumberFormat("en-ZA")`
- 🌗 **Light & dark mode toggle** — respects `prefers-color-scheme`, choice persisted to `localStorage`

## Run

**Web app (TanStack Start):**

```bash
bun install
bun dev
```

**Original Python pipeline:**

```bash
python src_py/advisor.py
```

## Project structure

```
src/routes/index.tsx           Web UI (upload, score, risks, recommendations)
src/lib/advisor.ts             TypeScript port of the 4-step pipeline
src/styles.css                 Design tokens incl. light/dark theme
data/sample_transactions.csv   Fictional April 2025 transactions
src_py/advisor.py              Offline 4-step pipeline (Python reference)
```

## The 4-step pipeline

1. **Categorise** — assign each transaction to a fixed category vocabulary.
2. **Summarise** — aggregate income, expenses, and per-category totals.
3. **Detect risks** — heuristic rules flag the top 3 risk areas with severity.
4. **Score & recommend** — transparent 0–100 score, explanation, 3 actions,
   and 1 quick win.

Every decision is human-readable. No black boxes.

## Theming

The app ships with a header `🌙 Dark / ☀️ Light` toggle. The choice is stored
in `localStorage("theme")` and applied by toggling the `.dark` class on
`<html>`, which switches the design tokens defined in `src/styles.css`.

## Reflection

Building the offline version forced me to make every "AI" step explainable
as plain code — which is exactly what a finance product needs for trust and
auditability. The same architecture plugs straight into an LLM by swapping
the four functions for prompt calls. Localising the currency to Rands and
shipping a proper light/dark mode were small but important polish steps for
a portfolio-ready demo.

**Disclaimer:** Educational prototype. Not financial advice. Uses fictional data.
