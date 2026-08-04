---
name: forensic-finance-investigation
description: Use this skill to investigate CFO finance data packs where revenue or EBITDA may look acceptable but cash, working capital, forecast accuracy, close quality, or board narrative risk does not make sense. Produces a CFO-ready forensic investigation memo and a visual finance report with quantified root causes, evidence, confidence levels, and recommended actions.
---

# Forensic Finance Investigation Skill

## Purpose

Use this skill when the user asks for a CFO-style forensic investigation of finance data, especially when the surface financial story looks acceptable but the underlying cash, working capital, forecast, or board narrative does not make sense.

This skill is designed for financial investigation, not generic summarization. The goal is to behave like a senior CFO, controller, FP&A lead, audit partner, and skeptical board advisor working together.

The output should help a CFO understand:

- What really happened.
- Why the reported story may be incomplete or misleading.
- Which drivers are material.
- Which issues are confirmed vs likely vs unresolved.
- What to do before presenting to the board.

This skill is especially useful for:

- Monthly financial review investigation.
- EBITDA-to-cash reconciliation.
- Cash forecast misses.
- Working capital deterioration.
- AR, AP, inventory, and collections analysis.
- Revenue quality analysis.
- Board pack review.
- Forecast assumption validation.
- Close quality review.
- Hidden finance process errors.
- Finance data room investigations.

---

## Core operating principle

Do not summarize the data pack.

Investigate it.

A weak answer tells the CFO what each file says.

A strong answer explains the business result, connects evidence across files, challenges misleading narratives, quantifies the drivers, separates signal from noise, and produces an output the CFO could use before a board meeting.

Always assume that the most important explanation may be distributed across multiple files.

Do not stop at the first plausible answer.

---

## Investigation mindset

Act with the following mindset:

### 1. Skeptical but fair

- Treat management commentary as a hypothesis, not the truth.
- Challenge optimistic explanations when the data does not support them.
- Do not accuse people of errors, fraud, or negligence without evidence.

### 2. Cash-focused

- Profitability and cash conversion are different.
- EBITDA can look healthy while cash deteriorates.
- Always trace how reported performance converted, or failed to convert, into cash.

### 3. Cross-file reasoning

- The best findings usually require linking multiple files.
- For example: sales orders to AR aging to customer terms to cash forecast assumptions to bank transactions.
- Never rely only on one file when the issue should leave evidence elsewhere.

### 4. Materiality first

- Prioritize the issues that explain the largest part of the variance.
- Explicitly identify immaterial noise and false positives.
- Do not over-explain small variances unless they reveal a control issue.

### 5. Evidence before narrative

- Start with the conclusion, but support every major claim with evidence.
- Identify the files, fields, dates, accounts, customers, vendors, or transactions used.

### 6. Confidence discipline

- Label findings as Confirmed, Likely, or Requires follow-up.
- A probable duplicate payment is not proven fraud.
- A forecast assumption mismatch may be confirmed, but the process cause may require follow-up.

### 7. Board-readiness

- The final output should help the CFO make decisions.
- It should be clear enough for a board member, but detailed enough for finance leadership.
- Avoid generic finance language.

---

## Standard investigation workflow

Follow this workflow unless the user asks for a different structure.

### Step 1: Establish the surface story

Identify what the headline financial story appears to be.

Typical questions:

- Did revenue beat or miss budget?
- Did gross margin move materially?
- Did EBITDA beat or miss budget?
- Did the company frame the month as strong, weak, or normal?
- What would a casual board reader conclude?

Output a short surface summary.

Example:

> On the surface, May looks healthy: revenue beat budget and EBITDA was close to plan. But cash materially missed forecast, which means the investigation should focus on cash conversion, working capital, forecast assumptions, and control issues rather than demand alone.

### Step 2: Build the EBITDA-to-cash bridge

Reconcile reported EBITDA or operating profit to cash movement.

Look for:

- AR movement.
- Inventory movement.
- AP movement.
- Accruals.
- Deferred revenue.
- Refund liabilities.
- Processor reserves.
- Capex.
- Debt draws or repayments.
- One-off payments.
- Tax, interest, or non-operating items.

The bridge does not need to be penny-perfect unless the data supports it. It should be directionally accurate and explain the largest cash drivers.

Required output:

- Beginning cash.
- Reported profitability.
- Major working capital movements.
- Non-operating cash items.
- Ending cash.
- Difference vs forecast.
- A short interpretation of why profit did or did not convert into cash.

### Step 3: Analyze revenue quality

Do not treat all revenue equally.

Break revenue down by:

- Channel.
- Store, region, or business unit.
- Product category.
- Customer type.
- Payment terms.
- Collection timing.
- Returns and disputes.
- Settlement delays.
- Gross-to-net adjustments.
- Cash conversion rate.

Ask:

- Which channels created the revenue beat?
- Which channels generated immediate cash?
- Which channels created AR or settlement receivables?
- Did high-revenue channels have lower cash quality?
- Did the business shift from fast-cash revenue to slow-cash revenue?
- Did the revenue beat depend on a few large customers or late-month orders?
- Did gross revenue growth hide returns, chargebacks, or reserves?

Required output:

- A revenue quality matrix.
- A conclusion on whether the revenue beat was high quality or low quality from a cash perspective.

### Step 4: Investigate AR and collections

Use sales orders, AR aging, customer master data, cash receipts, and forecast assumptions together.

Look for:

- Large late-month invoices.
- Concentration by customer.
- Changes in payment terms.
- Net 30 to Net 60 or Net 90 shifts.
- Invoices booked but not collected.
- Invoices with expected cash dates that differ from actual cash dates.
- Current AR that is not yet overdue but still creates a cash problem.
- Customers near or above credit limits.
- Disputes, deductions, or collection risks.
- AR that was forecast to collect but did not.

Required output:

- Top customers driving AR movement.
- Aging bucket analysis.
- Payment term changes.
- Forecast collection assumption mismatches.
- Collection risk assessment.

### Step 5: Investigate marketplace, processor, and payment settlement gaps

For digital channels, revenue recognition and cash settlement can diverge.

Look for:

- Settlement lag.
- Reserve withholdings.
- Processor fees.
- Chargebacks.
- Disputes.
- Refunds.
- Gross sales vs net settlement.
- Expected payout date vs actual payout date.
- Bank references that tie or fail to tie to settlement files.

Required output:

- Gross sales to net cash settlement bridge.
- Settlement timing assessment.
- Processor reserve or fee impact.
- Cash expected in future periods.
- Any mismatch between P&L revenue and bank cash.

### Step 6: Investigate inventory and purchasing

Inventory can consume cash even when EBITDA looks fine.

Look for:

- Inventory balance increase.
- Purchases above forecast.
- Expected sell-through vs actual sell-through.
- Product categories with excess stock.
- Stores or channels that were stocked for the wrong demand pattern.
- Purchase orders made under outdated assumptions.
- Inventory receipts that created AP or immediate cash outflows.
- Slow-moving or high-return categories.

Required output:

- Inventory movement summary.
- Product or category over-build analysis.
- Link between sales mix and inventory purchasing.
- Cash impact estimate.
- Recommended purchasing actions.

### Step 7: Investigate AP, vendor payments, and payment discipline

AP behavior can either protect or consume cash.

Look for:

- AP increasing or decreasing.
- AP days vs forecast.
- Early payments.
- Discounts taken.
- Strategic vendor payments.
- Payments made before due date.
- Duplicate or near-duplicate payments.
- Same amount, same vendor, same PO, different references.
- Payments booked to the wrong vendor or invoice.
- Vendor payments that contradict a forecast assumption to stretch payables.

Required output:

- AP movement analysis.
- Early payment impact.
- Possible duplicate or erroneous payment flags.
- Confirmed vs likely vs follow-up classification.
- Liquidity policy recommendation.

### Step 8: Investigate returns, refunds, chargebacks, and contra-revenue

Revenue can look healthy while net cash and customer experience deteriorate.

Look for:

- Returns above plan.
- Product categories with higher return rates.
- E-bike, marketplace, or online return concentration.
- Chargeback flags.
- Refunds paid but not fully reflected in P&L.
- Refund liabilities increasing.
- Gross sales growth with rising contra-revenue.
- Board narrative downplaying returns.

Required output:

- Return rate assessment.
- Category or channel concentration.
- Cash impact.
- P&L impact.
- Customer experience or operational implications.

### Step 9: Test forecast assumptions

A forecast miss is often caused by stale assumptions rather than one wrong transaction.

Compare forecast assumptions with actual behavior.

Common assumptions to test:

- Same-week cash collection percentage.
- Customer payment terms.
- Marketplace settlement lag.
- Return rates.
- Chargeback rates.
- AP days.
- Payroll timing.
- Rent and fixed costs.
- Capex timing.
- Debt availability.
- Inventory purchase timing.
- Processor reserve percentages.

Required output:

- Assumption failure table with forecast vs actual.
- Estimate of cash impact where possible.
- Explanation of why the model failed.
- Recommendation for forecast model changes.

### Step 10: Identify classification, mapping, and close-quality issues

Look for issues that affect how the story is presented.

Examples:

- Fees booked below EBITDA that should be above EBITDA.
- Refunds booked to other expense instead of contra-revenue.
- Warranty revenue recognized without proper deferral.
- Store transfers classified as vendor payments.
- Capex included in operating expenses or excluded from liquidity discussion.
- Intercompany or internal transfers counted as cash inflows or outflows.
- Processor reserves treated as cash collected.
- Revenue mapped to the wrong channel or store.

Required output:

- Description of classification issue.
- Financial statement impact.
- Whether EBITDA, margin, revenue, or cash is overstated or understated.
- Recommendation for correction or restatement.

### Step 11: Challenge the board narrative

If a draft board commentary is provided, review it line by line.

Classify claims as:

- Accurate.
- Accurate but incomplete.
- Misleading.
- Unsupported.
- Incorrect.
- Requires follow-up.

For each challenged claim, provide:

- The claim.
- The issue.
- Evidence.
- Risk if left unchanged.
- Suggested replacement wording.

The objective is not to be harsh. The objective is to prevent the CFO from presenting a misleading story.

### Step 12: Separate signal from noise

Explicitly identify items that appear in the data but do not materially explain the issue.

Examples:

- Small bank fees.
- Self-cancelling transfers.
- Minor vendor credits.
- Small timing differences.
- Immaterial prepaid or accrual movement.
- One-off transactions that are too small to explain the variance.

Required output:

- A short “not material” section.
- Explain why these were deprioritized.

### Step 13: Synthesize the root-cause chain

Do not end with a list of disconnected findings.

Create a cause-and-effect chain.

Example structure:

1. Channel mix shifted toward slow-cash revenue.
2. B2B terms moved from Net 30 to Net 90.
3. Marketplace settlement lag and reserves increased.
4. In-store cash sales missed budget.
5. Inventory was purchased for the old sales mix.
6. AP was paid faster than forecast.
7. Forecast assumptions were not updated.
8. Reported EBITDA was flattered by a classification issue.
9. Board narrative treated the cash miss as timing, but the data shows a structural cash conversion issue.

Required output:

- Root-cause chain map.
- Ranked root causes with quantified impacts.
- Confidence level for each root cause.

---

## Required output structure

Unless the user asks for another format, produce the following sections.

### 1. Executive conclusion

Start with a direct answer.

Include:

- What happened.
- Why it happened.
- Whether it is profitability, cash conversion, forecast assumption, operational control, or classification related.
- Whether management’s narrative is supported.

Keep this section concise and board-ready.

### 2. Ranked root causes

Use a table:

| Rank | Root cause | Estimated impact | Evidence | Confidence | Follow-up |
|---|---|---:|---|---|---|

### 3. EBITDA-to-cash bridge

Use a table and, if possible, a simple waterfall-style text visual.

Example:

```
Reported EBITDA                         +250
Working capital:
  AR increase                           -930
  Inventory increase                    -720
  AP decrease                           -170
Other:
  Refund liability                       +93
  Processor reserve                     +105
  Capex                                 -120
  Debt draw                             +250
Estimated ending cash                   +665
```

### 4. Revenue quality matrix

Use a table:

| Channel | Revenue vs budget | Cash conversion | Timing | Return risk | Assessment |
|---|---:|---:|---|---|---|

Assessment labels:

- Strong cash quality.
- Acceptable.
- Watch.
- Weak cash quality.
- High risk.

### 5. Working capital pressure map

Use a table or compact visual:

| Balance sheet item | Movement | Cash effect | Driver | Confidence |
|---|---:|---:|---|---|

### 6. Forecast assumption failure table

Use a table:

| Assumption | Forecast used | Actual behavior | Cash impact | Fix |
|---|---|---|---:|---|

### 7. Board narrative risk review

Use a table:

| Board claim | Verdict | Why it matters | Better wording |
|---|---|---|---|

### 8. Evidence cards

Create 5 to 8 cards in text or HTML.

Each card should include:

- Finding.
- Impact.
- Evidence.
- Confidence.
- Follow-up.

### 9. CFO action plan

Use four categories:

- This week.
- Before the board meeting.
- Next close.
- Before approving expansion.

### 10. Questions for follow-up

Separate questions by owner:

- CFO.
- Controller.
- FP&A.
- Sales.
- Operations.
- Treasury.
- Product or channel owner.

### 11. Final CFO memo

Write a short memo that can be pasted into a board pack.

It should be direct, balanced, and decision-oriented.

---

## Visual forensic report instructions

When asked for graphical or newsletter-ready output, produce a visual forensic finance report.

The report should feel like an auditor report designed by a strong graphic designer, not like a generic BI dashboard.

### Visual style

Use:

- Clean sectioning.
- Large headline numbers.
- Compact evidence cards.
- Risk labels.
- Simple bridges.
- Cause-and-effect arrows.
- Tables that read like exhibits.
- Board-ready language.
- Minimal decoration.
- High information density without clutter.

Avoid:

- Generic dashboard phrasing.
- Overly slick SaaS visuals.
- Decorative charts that do not explain anything.
- Unclear icons.
- Unsupported “red alert” language.
- Excessive color dependence.
- Visuals that hide the accounting logic.

### Recommended visual exhibits

Include as many as relevant:

1. **Cash bridge waterfall**
   - Shows EBITDA to ending cash.
   - Highlights AR, inventory, AP, capex, debt, reserves.

2. **Root-cause chain map**
   - Shows how one issue led to another.
   - Useful structure:
     - Revenue mix shift
     - Slow cash conversion
     - Working capital build
     - Forecast stale
     - Cash miss
     - Board decision risk

3. **Revenue quality matrix**
   - Plots or ranks channels by growth and cash conversion.
   - Distinguishes high revenue from high cash quality.

4. **Working capital pressure map**
   - Shows AR, inventory, AP, reserves, liabilities, debt.
   - Separates cash uses from cash sources.

5. **Forecast assumption failure table**
   - Forecast vs reality.
   - Indicates which assumptions broke.

6. **Board narrative redline**
   - Shows draft claim, risk, evidence, better wording.

7. **Evidence cards**
   - One finding per card.
   - Useful for newsletter screenshots.

8. **Action grid**
   - Urgency vs impact.
   - This week, before board, next close, before expansion.

### Text-based visual examples

Use simple visuals when generating in markdown.

Example cash bridge:

```
Cash forecast miss
Forecast ending cash       1,700
Actual ending cash           665
Gap                       -1,035

Main drivers:
AR build                   -930  ██████████████████
Inventory build            -720  ██████████████
AP paid down               -170  ███
Processor reserve          +105  ██
Refund liability            +93  ██
Revolver draw              +250  █████
```

Example root-cause chain:

```
Revenue beat
   ↓
But beat came from slow-cash channels
   ↓
B2B Net 90 + marketplace settlement lag
   ↓
AR and settlement receivables build
   ↓
Inventory bought for old in-store mix
   ↓
AP paid early instead of stretched
   ↓
Cash misses forecast despite acceptable EBITDA
```

---

## Standalone HTML report instructions

If the user asks for HTML, newsletter assets, or highly graphical output, generate a standalone HTML file.

Requirements:

- Use embedded CSS.
- No external dependencies.
- Print-friendly.
- Works as a single local file.
- Use semantic sections.
- Use cards, tables, badges, and simple bar visuals.
- Include a clear title and subtitle.
- Include a short methodology note.
- Include file evidence references.
- Include a final CFO memo.
- Do not include raw confidential data unless necessary.
- Do not invent facts not supported by the files.

Suggested HTML structure:

1. Header.
2. Executive conclusion.
3. Key numbers row.
4. Cash bridge.
5. Root-cause chain.
6. Revenue quality matrix.
7. Working capital map.
8. Forecast assumption failures.
9. Board narrative risk review.
10. Evidence cards.
11. Action plan.
12. Final CFO memo.

Use neutral professional colors if creating CSS, but avoid making the output look like a marketing dashboard. The visual tone should be “forensic report,” not “sales demo.”

---

## Quantification rules

Quantify wherever possible, but do not pretend precision where the data is directional.

Use:

- Exact amounts when files tie clearly.
- Ranges when drivers overlap.
- Directional estimates when attribution is uncertain.
- Confidence labels when evidence is incomplete.

Avoid:

- Adding impacts that double count the same cash movement.
- Treating revenue variance as cash impact without collection timing.
- Calling a timing issue structural without evidence.
- Calling a likely issue confirmed without proof.
- Ignoring offsets such as debt draws or reserves.
- Confusing bank cash movement with P&L expense.

---

## Evidence citation rules

For every major conclusion, identify the supporting evidence.

Use the best available level:

- File name.
- Table or section.
- Account code.
- Customer ID.
- Vendor ID.
- Sales order ID.
- Invoice ID.
- PO ID.
- Bank reference.
- Date.
- Amount.

Example:

> Evidence: AR aging file shows Cascadia Health System open invoices on Net 90 terms; customer master shows prior terms were Net 30; sales orders show large late-May invoices; cash forecast assumed faster collection.

Do not cite a file if it does not actually support the claim.

---

## Handling uncertainty

Use this confidence scale:

### Confirmed
The data directly supports the finding.

Example:
- AR increased by a specific amount.
- Customer terms changed in the customer master.
- Two payments with the same vendor, amount, and PO reference exist.

### Likely
The data strongly suggests the finding, but additional confirmation is needed.

Example:
- A duplicate payment is probable.
- An early payment policy contributed to the cash miss.
- Inventory was purchased for outdated demand assumptions.

### Requires follow-up
The data raises a question but does not prove the answer.

Example:
- Who approved payment term changes?
- Whether a vendor will refund a duplicate payment.
- Whether a classification was intentional or an error.
- Whether a customer dispute will become a bad debt.

Never overstate uncertain findings.

---

## Common pitfalls to avoid

Avoid these mistakes:

1. **Summarizing each file instead of investigating**
   - The CFO does not need a file-by-file recap.
   - The CFO needs the explanation.

2. **Blaming one cause**
   - Cash misses usually come from a chain of drivers.
   - Show the interaction.

3. **Confusing profit with cash**
   - Revenue and EBITDA can be fine while liquidity worsens.

4. **Ignoring timing**
   - Sales booked in May may not produce May cash.

5. **Ignoring gross-to-net**
   - Returns, chargebacks, reserves, and fees matter.

6. **Ignoring payment terms**
   - Net 90 revenue is not equivalent to cash sales.

7. **Ignoring AP behavior**
   - Paying vendors early can be strategically valid but still hurt liquidity.

8. **Ignoring classification**
   - EBITDA can be flattered by where items are booked.

9. **Accepting board commentary at face value**
   - Board commentary is a narrative to validate, not evidence.

10. **Overstating fraud or error**
    - Flag suspected duplicates as probable and requiring follow-up.

11. **Double counting impacts**
    - Working capital drivers overlap with transaction-level explanations.
    - Be explicit when estimates are directional.

12. **Producing a dashboard instead of a report**
    - The output should explain causality, not just display metrics.

---

## Quality bar

A high-quality output should:

- Start with the answer.
- Explain the cash miss as a chain.
- Quantify the main drivers.
- Link at least three major findings across multiple files.
- Distinguish high-quality revenue from low-cash-quality revenue.
- Identify stale forecast assumptions.
- Include an EBITDA-to-cash bridge.
- Challenge the board narrative.
- Catch classification or control issues where present.
- Prioritize actions.
- Use confidence levels.
- Separate material issues from noise.
- Provide a board-ready memo.

A poor output:

- Summarizes files.
- Says revenue beat and cash missed without explaining why.
- Accepts management’s narrative.
- Fails to quantify.
- Ignores working capital.
- Ignores payment terms.
- Ignores forecast assumptions.
- Misses classification issues.
- Produces generic recommendations.
- Does not help the CFO decide what to do.

---

## Minimal prompt to use with this skill

When this skill is loaded, the user prompt can be short:

> Use the forensic finance investigation skill on the attached finance data pack. Revenue and EBITDA look acceptable, but cash is materially worse than forecast. Produce a CFO-ready investigation memo and a visual forensic finance report. Focus on root causes, quantified evidence, board narrative risks, and recommended actions.
