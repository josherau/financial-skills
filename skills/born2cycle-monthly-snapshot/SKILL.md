---
name: born2cycle-monthly-snapshot
description: >-
  Generate the Born2Cycle CFO Monthly Financial Snapshot — the governed, fixed-design
  single-page HTML report (executive KPIs, revenue/GM/EBITDA trends, EBITDA bridge,
  liquidity and working capital, cash conversion cycle, business mix, cost-of-sales
  variance) built from the Finstory data-analysis MCP connector. Use this skill whenever
  the user asks for the monthly finance snapshot, CFO monthly snapshot, monthly
  financial report or pack, month-end reporting snapshot, or a snapshot for a named
  month and year for Born2Cycle — even if they only say "run the monthly snapshot" or
  mention NetSuite/Finstory monthly reporting. The layout, wording and formatting are
  fixed; only the reporting year and period vary. Do NOT design a new dashboard from
  scratch when this skill applies.
---

# Born2Cycle — CFO Monthly Financial Snapshot

This skill regenerates a **governed monthly deliverable**. The design, wording, chart
logic and number formatting are frozen in `assets/template.html` (bundled with this
skill). Your job is ONLY to: resolve the reporting period, run the query playbook
against the Finstory connector, validate the results, and inject one JSON object into
the template. Everything else (formatting, deltas, chart scales, labels) is computed by
the template's own JavaScript so that every month renders identically.

Why this matters: this file goes to the CFO. Two snapshots from different months must be
visually indistinguishable except for the numbers. Resist any urge to "improve" the
layout, reword labels, reformat numbers, or restyle charts — that would break the
month-over-month consistency the finance team relies on.

## Step 0 — Resolve the period and the connector

1. Call `get_company_context` on the Finstory data-analysis connector (tool names may
   carry a server prefix such as `mcp__` plus an id; if several servers expose this
   tool, use the one whose context describes **Born2Cycle**). From the response note:
   - the **defaultPov** (tenant's current reporting period),
   - available **year** members and **period** codes (`Jan` through `Dec`),
   - the **kpiLibrary** (must contain `Gross Margin %`, `EBITDA%`, `Current ratio`,
     `Quick ratio`, `DSO`, `DIO`, `DPO`, `Working capital as % net revenue`; if
     `Cash Conversion Cycle` is absent, it is governed as `DSO + DIO − DPO`).
2. Determine the reporting period:
   - If the user named a month/year (any format: "April 2026", "2026 P04", "Apr-26"),
     map it to the model's period code (`Apr`) and year (`2026`).
   - If the user did not name one, **use the Finstory defaultPov period and year** — do
     not guess from today's date and do not ask.
3. Define: `RY` = report year, `PY` = RY − 1, `P` = period code, `mi` = month index
   (Jan=0). Both `RY` and `PY` must exist as year members; if not, stop and tell the user.

## Step 1 — Query playbook (run all of these, nothing more)

Entity is always `Born2Cycle Group`, category `Actual` unless stated. Never re-derive a
governed KPI from components when the calculated member exists. Use these exact queries
(they are verified against the model):

| # | Purpose | template | params | pov |
|---|---------|----------|--------|-----|
| Q1 | Revenue by month, RY | `trend` | account `Revenue`, periods `Jan..P`, year RY | — |
| Q2 | Revenue by month, PY | `trend` | account `Revenue`, periods `Jan..Dec`, year PY | — |
| Q3 | GM% by month, RY | `trend` | account `Gross Margin %`, periods `Jan..P`, year RY | — |
| Q4 | GM% by month, PY | `trend` | account `Gross Margin %`, periods `Jan..Dec`, year PY | — |
| Q5 | EBITDA by month, RY | `trend` | account `EBITDA`, periods `Jan..P`, year RY | — |
| Q6 | Month P&L, Actual vs Budget | `snapshot` | accounts `["Revenue","Gross Profit","Gross Margin %","EBITDA","EBITDA%","Net Profit","Cost of Sales","Operating Expenses"]`, categories `["Actual","Budget"]` | `{year: RY, period: P}` |
| Q7 | Prior-year month P&L + ratios | `snapshot` | accounts `["Revenue","Gross Profit","Gross Margin %","EBITDA","EBITDA%","Net Profit","Cash Conversion Cycle","Working capital as % net revenue"]` | `{year: PY, period: P}` |
| Q8 | Cycle ratios, RY month | `snapshot` | accounts `["DSO","DIO","DPO","Cash Conversion Cycle","Working capital as % net revenue"]` | `{year: RY, period: P}` |
| Q9 | Closing balances, RY | `snapshot` | accounts `["10100","11000","12000","20000","Working Capital","Current ratio","Quick ratio"]` | `{year: RY, period: P, view: "YTD"}` |
| Q10 | Closing balances, PY | `snapshot` | same as Q9 | `{year: PY, period: P, view: "YTD"}` |
| Q11 | Revenue by entity | `breakdown` | dimension `entity`, member `Born2Cycle Group`, level `leaves`, account `Revenue` | `{year: RY, period: P}` |
| Q12 | GM% by entity | `breakdown` | same, account `Gross Margin %` | `{year: RY, period: P}` |
| Q13 | Gross profit by entity | `breakdown` | same, account `Gross Profit` | `{year: RY, period: P}` |
| Q14 | Cost-of-sales lines vs budget | `cross_tab` | row_dimension `account`, row_member `Cost of Sales`, row_level `children`, col_dimension `category`, col_members `["Actual","Budget"]` | `{year: RY, period: P}` |

Critical view semantics (this is the #1 mistake to avoid): the default `Periodic` view
returns **monthly P&L flows** — correct for Q1–Q8 and Q11–Q14. Balance-sheet **closing
balances require `view: "YTD"`** (Q9/Q10). The day/cycle ratios (DSO, DIO, DPO, CCC,
WC% of revenue) are governed RollingFY members and are view-independent — take them
as returned, never recompute from balances.

## Step 2 — Validate before building (stop-and-report policy)

The user has chosen: **never publish from partial data.** Stop and report (listing the
failing checks and raw query results) instead of producing the file if any of these fail:

- Q6 Actual `Revenue` or `Gross Profit` for the month is null, missing, or 0 — the
  month is not loaded.
- Q6 Budget `Revenue` or Budget `EBITDA` is null/0 — budget comparison impossible.
- Any month in Q1 (Jan..P) or Q2 (Jan..Dec) has null/0 revenue — a trend hole means
  the model is mid-load.
- Q9/Q10 return null for cash, inventory, receivables or payables.

Consistency ties (tolerance: $5,000 or 0.1pt). If one fails, re-check your transcription
before blaming the model; if it still fails, stop and report:

- Q6: `Gross Profit ≈ Revenue − Cost of Sales` and `EBITDA ≈ Gross Profit − Operating Expenses`.
- Bridge tie: `Budget EBITDA + (ActRev−BudRev) − (ActCoS−BudCoS) − (ActOpex−BudOpex) ≈ Actual EBITDA`.
- Q3's value for month P ≈ Q6's Actual `Gross Margin %`.
- Q11 revenue sum ≈ Q6 Actual Revenue (within $10K).

## Step 3 — Build the DATA object

Transcribe **raw values at full returned precision** (do not round, do not convert to
millions, do not multiply percentages — the template does all formatting). Percent-type
members come back as fractions (0.3688 = 36.9%); keep them as fractions.

```
{
  "year": 2026, "period": "May",
  "series": {
    "revenueRY": [Q1 values Jan..P, USD],
    "revenuePY": [Q2 values Jan..Dec, USD],
    "gmRY": [Q3 fractions], "gmPY": [Q4 fractions],
    "ebitdaRY": [Q5 values, USD]
  },
  "kpi": {
    "revenue":      {"a": Q6 Actual, "b": Q6 Budget, "p": Q7},
    "grossProfit":  {"a": ..., "b": ..., "p": ...},
    "grossMarginPct": {"a": ..., "b": ..., "p": ...},
    "ebitda":       {"a": ..., "b": ..., "p": ...},
    "ebitdaMarginPct": {"a": ..., "b": ..., "p": ...},
    "netProfit":    {"a": ..., "b": ..., "p": ...},
    "costOfSales":  {"a": Q6 Actual, "b": Q6 Budget},
    "opex":         {"a": Q6 Actual, "b": Q6 Budget}
  },
  "bs": {
    "cash": {"ry": Q9, "py": Q10}, "receivables": {"ry": ..., "py": ...},
    "inventory": {"ry": ..., "py": ...}, "payables": {"ry": ..., "py": ...},
    "workingCapital": {"ry": ..., "py": ...},
    "currentRatio": {"ry": ..., "py": ...}, "quickRatio": {"ry": ..., "py": ...}
  },
  "ratios": {
    "dso": {"ry": Q8}, "dio": {"ry": Q8}, "dpo": {"ry": Q8},
    "ccc": {"ry": Q8, "py": Q7}, "wcPctRevenue": {"ry": Q8, "py": Q7}
  },
  "entities": [
    {"code": "Born2Cycle Shops", "revenue": Q11, "gmPct": Q12, "grossProfit": Q13}, ...
  ],
  "cogsLines": [
    {"code": "Cost of Goods Sold", "actual": Q14, "budget": Q14}, ...
  ]
}
```

Join Q11/Q12/Q13 by entity code and Q14 rows by account display name, keeping the codes
and names verbatim as returned (the template maps display labels itself).

## Step 4 — Write the file and verify

1. Read `assets/template.html` from this skill's folder and write its content
   **verbatim, in full, changing nothing** to the output file, named
   `Born2Cycle_Monthly_Snapshot_` + period code + `_` + year + `.html`
   (e.g. `Born2Cycle_Monthly_Snapshot_May_2026.html`). The template contains the
   placeholder line `const DATA = __DATA_JSON__;`.
2. Replace `__DATA_JSON__` (one Edit) with the DATA object from Step 3.
3. Verify the written file: it must end with the init block calling `renderKpis();`
   through `renderCogsVar();`, contain `function renderTiles`, `function renderCCC`,
   `function renderEntity`, `function renderCogsVar`, `function waterfall`,
   `function bullet`, `function sparkline`, and no remaining `__DATA_JSON__`. If
   anything is off, rewrite the file — do not patch around transcription drift.
4. Present the file to the user with a short summary: headline KPIs (revenue, GM%,
   EBITDA vs budget and PY) and any validation notes. If the user hasn't set it up yet,
   you may offer (one line) to schedule this monthly.

## Fixed business mappings (encoded in the template — do not re-map yourself)

- Entity display names/order: Born2Cycle Shops → "Born2Cycle Shops"; Born2Cycle Retail →
  "Retail / Services"; Born2Cycle Tours → "Bike Tours"; Born2Cycle HQ → "HQ (central)";
  Born2Cycle Café → "Café"; Born2Cycle Online → "Online (direct)". Unknown new entity
  leaves are appended by the template under their model name — mention them in your summary.
- An entity whose GM% falls outside the −20%..80% axis (e.g. HQ) automatically shows its
  gross-profit drag label instead of a margin dot.
- Cost-of-sales display names: Cost of Goods Sold → "Core COGS"; Inventory Adjustments →
  "Inventory write-offs"; Aggregator & Payment Fees → "Marketplace & payment fees";
  Last-Mile Delivery & Vehicle → "Last-mile delivery"; Inbound Freight → "Inbound freight";
  Direct Personnel → "Direct personnel". Sorted by variance, most unfavourable first.
- The footnote about the 2025→2026 entity-mapping change renders **only when RY = 2026**.
- Cash and CCC have no governed budget → their Budget chips show "n/a" by design.

## Edge cases

- **January report**: series have one point; the template handles single-point
  sparklines and the "(Jan)" legend automatically.
- **Negative or near-zero comparison base** (e.g. April 2026 budget EBITDA is
  −$0.5M): a % change is meaningless, so money chips automatically fall back to the
  absolute $ delta (e.g. "▲ +$1.54M"), and the EBITDA bridge extends its axis below
  zero. Encoded in the template — no action needed, but sanity-check it in your summary.
- **CCC chip**: shown as flat (▬, grey) when the change is under 1 day; otherwise a
  *decrease* in CCC is favourable (green). The template encodes this — don't override.
- **Prior year must be complete** (12 loaded months) — else stop and report.
- If a query errors with "Member not found", use `search_members` to locate the member
  before concluding it doesn't exist; report if truly absent.
