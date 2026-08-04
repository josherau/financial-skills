# MFR Analysis Playbook

## Goal

The Monthly Financial Review is not a report summary. It is a management review that answers:

1. What changed?
2. Why did it change?
3. Does it matter?
4. What decision or follow-up is required?
5. What should be revisited next month?

For this skill, the MFR is a guided review followed by a repeatable HTML dashboard deck.

## Evidence hierarchy

Use evidence in this order:

1. Uploaded finance and operating driver workbooks.
2. Active Claude Project instructions.
3. Explicit user answers during review cycles.
4. General finance judgment.

Never reverse the hierarchy. General finance judgment cannot override the files. Project context cannot override actual results. User context can explain a result, but it should be marked as management input when not directly visible in the files.

## Common input patterns

Finance files often vary by company. Infer structure flexibly.

Common financial data:

- Actuals by month.
- Budget.
- Forecast or reforecast.
- Prior month.
- Prior year.
- YTD.
- P&L by account, department, region, entity, product, channel, or cost center.
- Cash and working capital.
- Headcount and personnel cost.

Common operating data:

- Units, customers, usage, transactions, orders, bookings, pipeline, visits, capacity, hours, or utilization.
- Revenue by product, segment, geography, channel, customer type, or business unit.
- Marketing funnel, sales funnel, churn, retention, expansion, pricing, discounting, or mix.
- Operational capacity, service levels, delivery cost, inventory, fulfillment, production, or compute.

## Core calculations

### Variance

For revenue and profit metrics:

- Favorable variance usually means actual above comparison.
- Unfavorable variance usually means actual below comparison.

For expenses:

- Actual above budget or forecast is usually unfavorable.
- Actual below budget or forecast is usually favorable.
- Check the account type before labeling.

For working capital:

- Do not automatically call higher inventory, AR, or deferred costs unfavorable.
- Interpret based on company context, seasonality, growth, timing, and cash implications.

### Common comparisons

Prefer the comparison that best answers the current question:

- Actual vs Budget: planning discipline.
- Actual vs Forecast: latest expectation accuracy.
- Actual vs Prior Month: momentum and trend breaks.
- Actual vs Prior Year: growth and seasonality.
- YTD: cumulative performance.

If multiple comparisons are available, do not show all of them by default. Use the one that supports the current review question.

### Materiality

Use Project context if it defines thresholds. Otherwise apply these practical defaults:

- Revenue, expense, or driver variance above 5 percent and meaningful in dollars or units.
- Gross margin or contribution margin movement above 100 basis points.
- EBITDA, operating income, or cash flow variance above 10 percent or material in dollars.
- Cash movement above 5 percent of beginning cash.
- Working capital movement above 10 percent.
- Any variance that changes a management decision, forecast, capacity plan, or risk view.

Materiality is not only math. A small variance can be material if it affects strategy, covenants, runway, forecast credibility, customer trust, or operational capacity.

## Finance interpretation modules

### Revenue or value drivers

Possible causes:

- Volume.
- Price.
- Mix.
- Channel.
- Product or service line.
- Region.
- Customer segment.
- New customers.
- Expansion or retention.
- Usage intensity.
- Promotions or discounting.
- Timing of orders, billing, implementation, delivery, or consumption.

If the files do not contain direct evidence of cause, label it as a hypothesis.

### Margin

Possible causes:

- Product, service, customer, or channel mix.
- Discounts or promotions.
- Input cost changes.
- Labor utilization.
- Capacity utilization.
- Supplier pricing.
- Freight, logistics, hosting, compute, support, or delivery costs.
- Returns, warranty, shrink, write-downs, credits, or one-time adjustments.

Margin explanations need driver evidence. A P&L variance alone can identify symptoms, not causes.

### Profit conversion

The CFO question is usually:

"Did revenue or activity upside convert into profit?"

Break the answer into:

1. Revenue or volume effect.
2. Margin rate effect.
3. Opex effect.
4. Headcount or investment effect.
5. One-time or timing items.
6. Net profit result.

Do not imply causality unless supported.

### Cash and working capital

Cash can diverge from profit because of:

- Inventory build.
- AR collections.
- AP timing.
- Deferred revenue.
- Customer prepayments.
- Capex.
- Debt, equity, or financing activity.
- Accruals vs cash timing.
- Seasonal stocking or capacity preparation.
- Supplier prepayments.
- Tax or payroll timing.

Ask the user for business context when the files do not show intent.

### Forecast implications

An MFR should not stop at explanation. It should connect the month to the forward view.

Ask:

- Does this result change the forecast?
- Was the variance timing or run-rate?
- Did the month validate or challenge the plan assumptions?
- Does the company need to change pricing, capacity, hiring, spend, or capital allocation?

## Output discipline

Use concise CFO language.

Separate:

- Confirmed facts.
- Likely explanations.
- Open questions.
- Management decisions.
- Follow-ups for next month.

Never invent causes, owner names, business events, or strategic conclusions not supported by the files, Project context, or user input.
