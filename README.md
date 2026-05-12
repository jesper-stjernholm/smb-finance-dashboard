# SMB Finance Dashboard

A transaction analytics dashboard for accounting professionals advising small and medium businesses. Upload a CSV of transactions or simulate a bank connection, and get an instant breakdown of cash flow, top movements, spending patterns, and recurring payments — all processed locally in the browser.

**Live demo:** [jesper-stjernholm.github.io/smb-finance-dashboard](https://jesper-stjernholm.github.io/smb-finance-dashboard/)

---

## What it does

The dashboard parses transaction data and renders a structured overview across five sections:

- **Overview** — monthly cash flow and overall cost breakdown
- **Top movements** — five largest expenses, five largest incomes, and largest income by client
- **Spending patterns** — fixed vs variable expenses (auto-detected) and average expense by day of week
- **Time patterns** — week-by-week expenses, running cash balance with 30-day forecast, and a daily activity heatmap
- **Recurring transactions** — automatically detected recurring payments with monthly median amounts

## Key design choices

**Local-only processing.** No API calls, no external services, no data leaves the browser. The entire analysis runs client-side in JavaScript, which makes it safe to publish publicly and fast to use.

**Smart heuristics over manual tagging.** Rather than requiring the user to categorise transactions, the app auto-classifies based on:

- **Fixed vs variable**: a transaction is "fixed" if its description (normalised) repeats across ≥2 months with amounts within ±15% of the median
- **Categories**: keyword rules covering payroll, tax/VAT, rent, software, marketing, contractors, travel, insurance, finance, office, utilities, meals, legal, and client revenue
- **Counterparties**: extracted by stripping common prefixes ("Client invoice –", "Contractor invoice –") so each entity aggregates correctly

**Tolerant CSV parser.** Handles ISO and European date formats, comma or semicolon delimiters, quoted fields, and mixed thousand/decimal separators. Expected columns: date, description, amount.
 VAT alerts, advisory nudges, and benchmark observations. The two are designed to be complementary: this app gives you the numbers, the other gives you the narrative.

## Running locally

It's a single HTML file with no build step. Either:

- Open `index.html` directly in any modern browser, or
- Visit the live demo linked above

External dependencies (Chart.js and the date adapter) are loaded from CDN.

## Tech

- Vanilla HTML, CSS, and JavaScript — no framework, no build tooling
- [Chart.js](https://www.chartjs.org/) for the charting
- DM Serif Display and DM Sans for typography
