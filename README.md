# KEEL — Household Cash Flow & Wealth Planner

A single-file budget instrument. Drag the levers, watch the waterline, find the tight weeks, and see what today's surplus becomes over 30 years.

Built from the household ledger:

- **Paychecks** — $3,030 after tax, every other Thursday (anchored to Jul 16 2026)
- **Stock distributions** — $4,400 quarterly (next Sep 8 2026)
- **Annual bonus** — $10,000 minimum, second Thursday of May
- **Monthly spend** — $8,054.87 across nine categories, line items preserved
- **Two loans, tracked separately** — $8,435 @ 1.0% due Oct 2027, and $30,000 @ 7.1% on a 10-year term

## Features

- **The Waterline** — a daily 12-month projection of cash on hand. Your actual budget rides along as a dashed ghost line so every slider move shows its wake instantly. Weeks that dip below your comfort buffer are flooded red and listed as tight-water chips.
- **The Ballast** — each loan gets preset buttons (**Interest only**, **Minimum** to meet the deadline, and quick payoff timeframes) plus a payment slider ranging from interest-only up to a ~5× faster payoff. Live readouts show the payoff date, total interest, standing vs deadline, and the payment that gets freed. Interest-only courses are modeled honestly: the remaining balance survives to term as a balloon, which is paid out of the portfolio on the wealth trajectory (the ▼ notch) — so interest-only-and-invest can be compared fairly against paying down. Payoffs are flagged on the waterline, and freed payments flow back into the surplus the month each loan clears.
- **The Levers** — sliders for every income source and spend category, with expandable line-item detail pulled straight from the spreadsheet. Deltas from your actuals show in green/red as you drag.
- **Bill timing** — model bills hitting all on the 1st, split 1st & 15th, or spread daily.
- **The Long Game** — invests your monthly surplus at an adjustable return and projects 10/20/30-year outcomes, separating contributions from compound growth.
- **The Ledger (`ledger.html`)** — the source of truth, linked from the header. Every income figure, spend line item (rename, re-amount, add, delete), and loan balance/rate is directly editable with live totals. Hitting **Save ledger** makes those values the new "actuals" that KEEL's sliders, ghost line, and charts anchor to.
- Scenario state persists in your browser (`localStorage`). **Reset to actuals** restores the ledger numbers.

## How persistence works (and why)

GitHub Pages is a static host — there's no server or database on any plan — so KEEL is built **local-first**, the standard architecture for world-class apps in this space:

- The ledger and your scenario positions live in the browser's `localStorage`. This survives refreshes, browser restarts, and site redeployments, and nothing ever leaves your device.
- **Export** downloads your ledger as a `keel-ledger.json` backup; **Import** loads it on another device or browser. This is your cross-device sync and your safety net.
- Saving the ledger bumps a revision number; the main page detects it and re-anchors sliders to the new actuals automatically.
- One caveat to know: storage is per-browser, per-device, and clearing site data clears the ledger — keep an exported JSON if the numbers matter.

No build step, no dependencies, no accounts, no data leaves the browser.

## Deploy to GitHub Pages

1. Create a new repository (e.g. `keel`), public.
2. Upload `index.html`, `ledger.html`, and this `README.md` to the repository root.
3. Repo **Settings → Pages → Source**: select **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. In a minute or two the site is live at `https://<your-username>.github.io/keel/`.

To update numbers later, edit the `BASE` object at the top of the `<script>` block in `index.html` — every figure, line item, and loan lives there (loans are in `BASE.loans` with balance, rate, and deadline).

## Anchors & assumptions

- Bills debit per the selected timing mode; income lands on its real calendar dates.
- The wealth projection assumes a steady average annual return, monthly compounding, and no taxes on growth — a planning instrument, not financial advice.
