---
name: cfo-cash-dashboard
description: Use this skill to turn a controlled cash reconciliation pack into a CFO-ready dashboard. It inspects the reconciliation output, treats reconciled/dashboard-ready data as the source of truth, adapts to different workbook structures, visualizes cash movement, bank-vs-ERP differences, exceptions, drivers, and AR/AP context, and produces a polished executive dashboard without redoing the reconciliation unless the pack is incomplete or inconsistent.
---

# CFO Cash Dashboard Skill

## Purpose

Use this skill to convert a completed cash reconciliation pack into a CFO-ready dashboard and short executive narrative.

The skill is designed for finance workflows where the reconciliation has already been performed. The dashboard should make the control story visible: actual cash position, entity-level reconciliation status, material exceptions, key cash drivers, and near-term AR/AP cash context.

This skill must be generic and reusable across companies. Do not hardcode company names, dates, entities, bank names, categories, sample values, email addresses, or file names.

## Core principle

The reconciliation pack is the controlled source of truth.

Use the pack's dashboard-ready data, reconciliation tables, exception log, cash driver commentary, and executive summary wherever available.

Do not recalculate the reconciliation from raw bank, ERP, AR, or AP files unless:

- The reconciliation pack is missing required data.
- The dashboard-ready data conflicts with the reconciliation tables.
- The user explicitly asks for a recalculation.

If conflicts are found, flag them visibly and ask a concise clarification question before finalizing the dashboard if the choice materially changes the message.

## Input inspection

Inspect the uploaded files before building the dashboard.

Identify the likely role of each file based on structure and content, not file name alone:

- Cash reconciliation pack
- Dashboard-ready data file
- Executive summary
- Exception log
- Raw bank statement
- ERP cash GL export
- AR/AP aging export
- Existing dashboard or prior report
- Other supporting file

Within a workbook, identify relevant sheets semantically. Prefer sheets or sections containing:

- Executive summary
- Dashboard-ready data
- Cash reconciliation by entity/account/consolidated
- Bank vs ERP reconciliation
- Exception log
- Cash drivers
- AR aging summary
- AP aging summary
- Normalized bank transactions
- Input log

Do not assume exact sheet names. Common equivalents include names such as Summary, Dashboard Data, Reconciliation, Bank to GL, Exceptions, Drivers, AR, AP, Open Items, and Cash Bridge.

## Multiple-choice clarification rules

Ask concise multiple-choice questions only when the answer materially affects the dashboard's numbers, message, or output format.

Use multiple-choice questions instead of broad open questions whenever practical.

Each question should have:

- One clear decision to make
- Three to five answer choices labeled A, B, C, D, and optionally E
- A recommended default if one option is safest for CFO reporting
- A short explanation of why the choice matters

Good clarification moments include:

- Multiple possible source-of-truth tables are present.
- Reported cash, ERP cash, and corrected/reconciled cash conflict.
- The dashboard-ready data is incomplete or inconsistent with the reconciliation table.
- The user has not specified output format and multiple useful formats are possible.
- A material assumption changes the headline message.
- A dashboard is intended for different audiences, such as CFO review, board review, treasury operations, or audit/control review.

Do not ask about minor formatting preferences. Use professional CFO defaults.

If the user does not answer, proceed with the most conservative finance reporting choice, document the assumption, and surface the assumption on the dashboard.

## Dashboard story hierarchy

Build the dashboard around the finance story, not around the available charts.

Use this hierarchy:

1. Headline cash position and reconciliation status.
2. Cash movement bridge from opening cash to reconciled ending cash.
3. Entity-level view of reported bank cash, ERP cash, and corrected/reconciled cash where available.
4. Bank-vs-ERP differences and whether consolidated totals hide entity-level issues.
5. High-severity exceptions and required follow-ups.
6. Top inflow and outflow drivers.
7. AR/AP near-term cash context.
8. Assumptions and limitations.

The dashboard should make the most important control issue visible within the first screen.

## Required dashboard components

Include these sections when the data is available:

### Executive headline

Show:

- Reporting period
- Reconciled ending cash
- Reported bank ending cash, if different
- ERP cash GL ending cash, if different
- Net cash movement
- Reconciliation status
- Number and severity of exceptions
- One-sentence CFO takeaway

### Cash bridge

Show a visual bridge from opening cash to ending cash:

- Opening cash
- Major inflow groups
- Major outflow groups
- Net adjustments, if applicable
- Reconciled ending cash

If a waterfall chart is difficult to produce, use a bar bridge or clearly labeled table that preserves the bridge logic.

### Entity reconciliation

Show cash by entity/account where available:

- Bank statement ending cash
- ERP cash GL ending cash
- Corrected or reconciled ending cash
- Difference amount
- Difference explanation status

Do not allow a small consolidated difference to hide material entity-level issues. If entity-level issues offset, call this out explicitly.

### Exception summary

Show:

- High/medium/low exception counts
- Amount at risk by severity, if available
- Top exceptions with entity, amount, likely cause, and recommended follow-up
- Status or owner, if available

Keep exceptions visible. Do not bury them in footnotes.

### Cash drivers

Show the main drivers of cash movement:

- Top inflows
- Top outflows
- Major recurring payments
- Major unusual or one-off transactions
- Entity or category contribution

Tie driver commentary to source data from the reconciliation pack.

### AR/AP cash context

Where available, show:

- Near-term expected AR receipts
- Overdue AR requiring follow-up
- Near-term AP obligations
- Paid AP items still open or other payment-control conflicts
- Cash risks for the next one to two weeks

### Assumptions and limitations

Show material assumptions directly on the dashboard or in a clearly visible notes panel.

Examples of assumptions:

- Which cash figure is treated as reconciled or corrected cash
- Duplicate treatment
- Missing ERP posting treatment
- Timing difference treatment
- Materiality threshold

Do not hide assumptions in invisible metadata.

## Visual design rules

Use a clean, executive CFO style:

- Clear title and reporting period
- One strong headline message
- Metric cards for the most important numbers
- Charts that answer specific questions
- Short labels and readable numbers
- Tables only where detail matters
- Consistent number formatting
- Explicit signs for cash increases and decreases
- Conditional emphasis for exceptions and risks
- Minimal decoration

Prefer these visuals:

- Waterfall or bridge for cash movement
- Grouped bar chart for Bank vs ERP vs Reconciled cash by entity
- Horizontal bar chart for top inflows/outflows
- Stacked or simple bar chart for exception severity
- Table for top exceptions and follow-ups
- Timeline or compact table for AR/AP near-term items

Avoid:

- Decorative chart clutter
- 3D charts
- Pie charts unless showing a simple composition with few categories
- Unsupported commentary
- Dense dashboard pages that require scrolling before the headline is visible

## Output format

Default output when file creation is available:

- A self-contained HTML dashboard named clearly with the dashboard purpose and reporting date.
- The HTML should not require external data files to render.
- Include the key underlying dashboard data in the HTML as embedded structured data, table markup, or clearly visible tables.

If the user or environment prefers spreadsheets, also create or update an XLSX dashboard tab using the reconciliation pack as the data source.

If HTML is created, it should be presentation-ready and include:

- Executive headline section
- KPI cards
- Visual charts
- Exception table
- Driver table or driver cards
- AR/AP context
- Assumptions and limitations
- Footer identifying the source reconciliation pack

Use responsive layout so the dashboard works in a browser screenshot for newsletter use.

## Executive narrative

In addition to the dashboard, write a short executive summary in plain language:

- What is the reconciled cash position?
- What is the headline reconciliation issue?
- What drove cash movement?
- What exceptions need CFO attention?
- What should finance do next?

Keep the narrative concise. Do not repeat every table.

## Quality gates

Before finalizing, check that:

- The reconciliation pack or dashboard-ready data was inspected.
- Dashboard numbers tie to the controlled reconciliation pack.
- The source of truth is documented.
- Reconciled/corrected cash is clearly distinguished from bank-reported and ERP-reported cash where they differ.
- Entity-level issues are visible, not hidden by consolidated totals.
- High-severity exceptions are shown prominently.
- Cash driver commentary is supported by data from the pack.
- AR/AP context is not presented as actual cash unless clearly labeled as expected or open.
- Material assumptions are visible.
- The dashboard can be understood without the user opening the workbook.

## Boundaries

Do not create or submit payment files.
Do not send emails.
Do not move money.
Do not post journal entries.
Do not change source files unless explicitly asked.
Do not use raw source files as the dashboard source of truth when a controlled reconciliation pack is available.
Do not silently override reconciled numbers with recalculated numbers.
Do not hide material reconciliation issues behind a clean consolidated headline.
Do not invent explanations that are not supported by the reconciliation pack.
