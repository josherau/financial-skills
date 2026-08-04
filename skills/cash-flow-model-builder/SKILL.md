---
name: cash-flow-model-builder
description: Use this skill to build a simple Week 0 13-week cash flow forecast Excel model from messy finance exports. It is designed for newsletter demos and first-pass model creation. It aggregates source data into weekly schedules, creates a clean Excel workbook, flags material exceptions, and self-checks the model. It does not create a full row-level audit trail, detailed dashboard, or advanced scenario engine.
---

# Cash Flow Model Builder

## Purpose

Build a simple first version of a 13-week cash flow forecast from messy finance exports.

This is a **Week 0 model creation** skill. The goal is to create a clean downloadable Excel workbook that a CFO can review and later enhance with weekly update, audit trail, and dashboard skills.

## Primary output

Create a downloadable Excel workbook named:

`week0_13_week_cash_flow_forecast.xlsx`

The Excel workbook is the main deliverable. Do not only provide tables in chat unless file creation is unavailable.

Keep the workbook demo-friendly. Use no more than these tabs:

1. `README`
2. `Input Inventory`
3. `Weekly Schedules`
4. `13-Week Forecast`
5. `Exceptions`
6. `Self-Check`
7. `CFO Summary`

The chat response should only provide a short summary of what was created and important review items.

## Scope

Assume:
- One company.
- One legal entity.
- One reporting currency, USD unless otherwise stated.
- One primary operating bank account.
- 13 weekly forecast periods.

Do not model:
- Multi-entity consolidation.
- Multiple bank accounts.
- Multi-currency or FX translation.
- Intercompany cash transfers.
- Covenant modeling.
- Advanced scenario dashboards.
- Full row-level audit trail.

If the files suggest these complexities, mention them as out of scope.

## Core instruction

Keep the model simple.

Do **not** build a full row-level audit trail.
Do **not** build a detailed scenario engine.
Do **not** create a large workbook with many supporting tabs.
Do **not** try to preserve every source row in the workbook.

Instead:
1. Inspect the uploaded files.
2. Summarize what each file contributes.
3. Aggregate source data into weekly cash inflow and outflow schedules.
4. Build a clean 13-week cash forecast.
5. Flag material exceptions and data issues.
6. Self-check the forecast before finalizing.

## Workflow

### Step 1 — Inventory the files

Create an `Input Inventory` tab.

For each uploaded file, identify:
- File name.
- File type.
- Approximate row count.
- Date range.
- Main columns.
- Forecast use.
- Used / partially used / not used.
- Key data quality issues.

Keep this concise.

### Step 2 — Set the forecast calendar

Determine the as-of date from the files or user prompt.

Prefer:
1. User-provided date.
2. Export date in file names.
3. Latest bank transaction date.
4. Latest export timestamp.

Create 13 weekly forecast buckets starting from the as-of date or the next logical week start.

Use clear week labels:
- Week 1
- Week 2
- ...
- Week 13

Each week should have a start date and end date.

### Step 3 — Determine opening cash

Use the latest available running balance from the bank transaction export.

Rules:
- If there are multiple transactions on the latest date, use the final running balance after all same-day transactions.
- If the latest bank balance is unclear, flag this as a major exception.
- Do not use CFO notes as opening cash unless no bank data exists.

### Step 4 — Build weekly inflow schedules

Aggregate inflows by week and category.

Use practical cash timing:
- Card settlements / retail payouts: expected payout date if available; otherwise short delay from transaction/order date.
- Online and marketplace payouts: expected payout date if available.
- AR collections: expected collection date first, due date second.
- Overdue AR with no expected date: estimate conservatively and flag.
- Disputed AR: exclude from base forecast unless clearly marked as promise-to-pay or explicitly supported by notes.
- Avoid double-counting B2B sales if the same customer amount appears in AR.

Required weekly inflow categories:
- Retail / card settlements
- Online / marketplace payouts
- AR collections
- Other receipts

### Step 5 — Build weekly outflow schedules

Aggregate outflows by week and category.

Use practical cash timing:
- AP: due date.
- AP with missing due date: do not schedule automatically; flag in exceptions.
- AP with hold flag: exclude from base forecast and flag.
- Payroll: scheduled pay run date.
- Recurring payments: next payment date.
- Tax and debt: scheduled date.
- Purchase orders: include only near-term, material, open/approved/partially received commitments. Exclude cancelled POs.
- Avoid double-counting POs already present in AP.

Required weekly outflow categories:
- Payroll and benefits
- Inventory / vendor payments
- Operating AP
- Recurring payments
- Rent and facilities
- Marketing / discretionary spend
- Tax
- Debt service
- Purchase commitments
- Other disbursements

### Step 6 — Create the `Weekly Schedules` tab

Create one supporting tab that shows weekly aggregated schedules.

Include:
- Inflows by week and category.
- Outflows by week and category.
- Key assumptions used.
- Excluded items summary.

This tab should support the forecast without becoming a detailed database.

### Step 7 — Create the `13-Week Forecast` tab

Create a clean 13-week cash forecast.

Minimum lines:
- Opening cash
- Retail / card settlements
- Online / marketplace payouts
- AR collections
- Other receipts
- Total cash receipts
- Payroll and benefits
- Inventory / vendor payments
- Operating AP
- Recurring payments
- Rent and facilities
- Marketing / discretionary spend
- Tax
- Debt service
- Purchase commitments
- Other disbursements
- Total cash disbursements
- Net cash flow
- Ending cash
- Minimum cash / below-threshold flag

Use positive values for receipts and disbursements in separate sections.

Roll-forward rule:
`Ending cash = Opening cash + Total cash receipts - Total cash disbursements`

Next week opening cash must equal the prior week ending cash.

Default cash threshold: $750,000 unless provided by the user.

### Step 8 — Create an `Exceptions` tab

Flag only material or important issues.

Include:
- Missing due dates.
- Duplicate bank references.
- Disputed AR.
- Held AP.
- Large unusual transactions.
- Missing opening cash if applicable.
- Potential double-counts.
- Cancelled or backordered POs.
- Any assumption made because data was incomplete.

For each exception, include:
- Issue type.
- Source file.
- Source reference if available.
- Amount if relevant.
- Forecast treatment.
- CFO review required: Yes / No.

Do not list thousands of minor items. Keep the exceptions tab readable.

### Step 9 — Create a `Self-Check` tab

Before finalizing, verify the model.

Required checks:
- Opening cash ties to latest bank running balance.
- Weekly roll-forward works.
- Week-to-week opening cash equals prior week ending cash.
- Receipts and disbursements are not sign-flipped.
- Held AP is excluded from the base forecast.
- Disputed AR is treated conservatively.
- Cancelled POs are excluded.
- Payroll, tax, rent, and debt service are not treated as deferrable.
- Material forecast lines have source support or a documented assumption.
- Any unresolved issue is listed in `Exceptions`.

Use status:
- PASS
- WARNING
- FAIL

If any material FAIL remains, label the workbook as a draft requiring CFO review.

### Step 10 — Create a `CFO Summary` tab

Summarize:
- As-of date.
- Opening cash.
- Forecast ending cash after 13 weeks.
- Minimum cash week and amount.
- Number of weeks below threshold.
- Biggest cash inflow risks.
- Biggest cash outflow risks.
- Most important exceptions.
- Whether the model is ready for CFO review.

Keep the tone practical and conservative.

## If generation is taking too long

If processing all files in full detail would make the task too large:
1. Aggregate first.
2. Use materiality thresholds.
3. Include source-level detail only for exceptions.
4. Continue building the workbook instead of expanding analysis in chat.

Do not get stuck trying to create a full audit trail, detailed dashboard, or full scenario model.

## Final response

When finished, respond with:
- Link to the Excel workbook.
- 3–5 bullet summary.
- Any material warnings.

Do not provide a long explanation in chat.
