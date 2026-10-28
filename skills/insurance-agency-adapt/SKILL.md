---
name: insurance-agency-adapt
description: Install a CFOS-style 8-step financial operating system at an independent insurance agency (P&C, benefits, life), adapted from the CFOS construction system.
---

# Insurance agency financial operating system

Use this skill to install a monthly financial operating system at one named independent insurance agency or brokerage. It keeps the CFOS (runoncfos.com) spine: one cost language, a true overhead picture, priced work, aligned software, service standards, a monthly cadence, and owner accountability. It replaces the parts that assume job cost, equipment and WIP. For contractors and field-service businesses use `cfos-client-adapt` instead.

The output is always three things:
1. **Fit assessment**: agency profile, which steps apply, and the data gaps.
2. **Install plan**: a Claude Doc with each step's deliverable, owner, inputs and dates.
3. **Adapted workpapers**: a book-of-business P&L, a comp-ratio build, producer economics, a trust reconciliation, and a renewal-driven cash forecast. Every number is traced to agency data or labelled as an estimate.

## Ground rules

- Agency actuals, benchmarks and estimates stay in separate columns. Label every figure with its source and period.
- Never send agency data outside the firm.
- Revenue recognition under ASC 606, contingent-commission accrual policy, producer classification (W-2 or 1099), and state trust-account rules belong to the agency's CPA and counsel. Flag them, don't decide them.
- If a number is missing, list it as missing. Never fill the gap with a plausible figure.
- Benchmarks below are from the Big "I" / Reagan Consulting Best Practices Study. Those are **top-performing agencies**, not the industry average. Say so whenever you compare.

## Step 0. Intake and agency profile

| Item | Why |
| --- | --- |
| 13 months of P&L and balance sheet by month | Margins, comp ratio, trend |
| Revenue by line (commercial P&C, personal lines, group benefits, life/health, other) and by carrier | Book P&L, carrier concentration |
| Split of revenue into new business and renewal, by producer | Producer economics, organic growth |
| Commission statements: direct-bill and agency-bill, and contingent or profit-sharing history for 3 years | Revenue reconciliation and accrual |
| Payroll register by person and role (producer, account manager/CSR, sales support, admin, owner) with the comp plan | Comp ratio, validation |
| Premium trust account bank statements and the agency management system (AMS) trust ledger | Fiduciary reconciliation |
| Policy and client retention by line for 2 years | Organic growth driver |
| AMS in use (Applied Epic, AMS360, HawkSoft, EZLynx, other) and general ledger | Step 05 |
| Debt, earn-outs from acquisitions, book purchase notes | Cash and valuation view |
| Renewal calendar by month (premium and commission) | Seasonal cash forecast |

Classify the agency:

| Profile | Revenue driver | What matters most |
| --- | --- | --- |
| Commercial-heavy P&C | Large accounts, agency bill common | Producer validation, trust accounting, contingents |
| Personal lines | High volume, mostly direct bill | Retention, accounts per CSR, cost per policy |
| Benefits | Per-employee per-month fees and commissions | Retention, renewal timing (1/1 heavy) |
| Mixed / aggregator member | Mix of the above, often via a network or cluster | Commission splits with the network, carrier access |

## The 8 steps, adapted

Critical path: 01, then 03, then 04. 05 starts once 01 is defined. 06 needs 01. 07 needs 03 to 06. 08 needs 03, 06 and 07.

### 01 Revenue and cost structure (replaces job cost)

One revenue language across the AMS, the ledger and producer comp.
- Revenue segments: line of business × new or renewal × billing type (agency bill, direct bill). Contingent and profit-sharing, fee income and interest on trust funds (where the state lets the agency keep it) each go on their own line.
- Report **net revenue**: commissions and fees minus commissions paid to sub-producers or networks. Ratios below run on net revenue.
- Cost groups:
  - producer comp (salary, commission, bonus)
  - service staff comp (account managers, CSRs)
  - sales support and marketing
  - admin and leadership comp
  - benefits and payroll tax, allocated to each group above
  - occupancy
  - technology (AMS, raters, comparative rating, phones)
  - E&O and other insurance
  - professional fees
  - travel and entertainment
  - other

Deliverable: a mapping from the current chart of accounts and AMS revenue codes to these segments.

### 02 Equipment cost basis

Drops. Technology cost per employee goes in step 03.

### 03 Overhead and comp ratio

- **Comp ratio = total compensation including benefits and payroll tax ÷ net revenue.** This is the agency's main cost metric. Compute it on the total and by group.
- Owner comp goes in at market rate for the role the owner actually performs (producer, leader, or both), even if paid as distributions. Then show the adjustment from reported EBITDA to **pro forma EBITDA**. Buyers use pro forma.
- Operating expense ratio = non-comp expense ÷ net revenue.
- EBITDA margin = net revenue − total comp − operating expense, ÷ net revenue.
- Productivity: net revenue per employee (headcount as full-time equivalents), and accounts or premium per service person.

### 04 Producer economics (replaces estimating)

What a producer costs against the book they write.
- **Validation**: a producer is validated when their book's commission at the standard commission schedule covers their actual pay. Show each producer's book and actual pay, and compute validation % = book commission at schedule ÷ actual pay.
- **Unvalidated producer payroll**: actual pay minus earned commission for producers not yet validated. That is the agency's investment in growth. Track it as a % of net revenue. Reagan calls the net version NUPP (net unvalidated producer payroll).
- **Book ownership**: who owns the book, the agency or the producer, and the non-solicit and vesting terms. Counsel reads the agreements.
- **Commission schedule check**: the new and renewal splits paid to producers against the agency's own targets. A renewal rate set too high cuts margin on the whole book.
- Account profitability for commercial accounts: commission minus service hours × burdened service cost. This shows which small accounts lose money.

### 05 Software and bookkeeping alignment

- The AMS is the source for revenue detail. The ledger must tie to it every month, by segment.
- Direct-bill commission: reconcile carrier statements to the AMS expected commission, policy by policy. Unmatched items are lost revenue or overstated receivables.
- Agency bill: receivables from insureds and payables to carriers must reconcile to the trust account (step 07).
- Revenue timing: under ASC 606 commission is generally recognized on the policy effective date, not when cash arrives, with an allowance for cancellations. Installment and audit premiums need a policy decision. CPA decides.
- Close by the 10th of the following month.

### 06 Service standards (replaces PM standards)

- Retention by line and by account manager, measured on revenue and on accounts.
- Accounts (or premium) per service person by line, against the agency's own target.
- Renewal workflow: remarketing starts at a set number of days before expiry, with the date the agency sets.
- New business pipeline: quoted, bound, and close rate per producer.
- Receivable standards for agency bill: invoice at binding, and a written rule for when overdue premium triggers a cancellation notice.

### 07 Monthly cadence

Monthly rhythm:
- Week 1: close and the trust reconciliation.
- Week 2: book-of-business P&L and producer report.
- Week 3: business report (P&L, balance sheet, KPIs, Rule of 20).
- Week 4: cash forecast.

Tools:
- **Premium trust reconciliation**, agency bill only.
  - The trust bank balance must equal unremitted premium owed to carriers plus commission earned but not yet swept to operating.
  - No commingling: operating money never goes in, trust money never pays operating costs.
  - Any shortfall goes to the owner the same day. It is a state regulatory issue, not just a cash issue. Counsel confirms that state's rules, including where the account must be held and who keeps the interest.
- **Cash forecast.** Use the CFOS 13-week workbook and its 24-month tab, but drive receipts from the renewal calendar, not from job billing.
  - Separate trust cash from operating cash. Only operating cash counts toward the floor.
  - Contingent commissions arrive once or twice a year. Forecast them as a separate line and never count on them to meet the floor.
  - Cash floor: 3–6× monthly operating expense (the CFOS rule).
- **Contingent accrual.** Each month estimate the contingent commission earned to date from carrier loss ratios, premium volume and growth against each carrier's agreement. Under ASC 606 it is variable consideration that is estimated and constrained, not booked when the check arrives. Show the accrual and its swing, because it moves EBITDA from one period to another.
- **Organic growth** = (net revenue this period − net revenue in the same period last year − revenue from acquisitions in the last 12 months + revenue from books sold) ÷ the prior-year net revenue. Exclude contingents, or show the figure both with and without them, and say which.
- **Rule of 20** = organic growth % + ½ × pro forma EBITDA margin %. A score of 20 or more is the healthy threshold Reagan uses.

### 08 Standards and accountability

About 5 owner hours a month. Each standard has one owner and one number, reviewed in the week 3 meeting. Sample standards:
- close by the 10th;
- trust reconciled by the 10th with zero unexplained difference;
- direct-bill commission variance cleared within 30 days;
- retention by line reviewed monthly;
- producer validation reviewed quarterly;
- contingent accrual re-estimated monthly.

## Benchmarks

Source: 2026 Best Practices Study (2025 data), Big "I" and Reagan Consulting, as reported by Insurance Business, 2026-08-13. These are top-performing agencies.

| Metric | Range across revenue bands |
| --- | --- |
| Organic growth | 6.2% to 10.2% (prior year: 8.7% to 11.3%) |
| Pro forma EBITDA margin | 23.2% to 30.7% |
| Rule of 20 median | 19.3 to 26.1 |

Comp ratio, revenue per employee, and NUPP benchmarks by revenue band are in the full study. Do not quote them until the agency or firm supplies the study. Never borrow construction benchmarks.

## How the CFOS construction rules translate

| CFOS rule | Agency version |
| --- | --- |
| 12% net profit target | Pro forma EBITDA margin and Rule of 20, from the benchmark above |
| Overhead rate | Comp ratio plus operating expense ratio |
| Price = cost ÷ (1 − GM) | Producer validation and the commission schedule |
| WIP and overbilling | Trust reconciliation and contingent accrual |
| Equipment rates | None |
| Working capital 10–15% of revenue | Operating cash floor at 3–6× monthly operating expense, with trust cash excluded |

## Install plan output

Write the plan as a Claude Doc titled "<Agency> financial operating system install plan". It has these sections:
1. Agency profile and fit.
2. Baseline: 13 months of net revenue, comp ratio, EBITDA (reported and pro forma), organic growth and Rule of 20, from agency data.
3. Targets, and the source of each one.
4. Step-by-step deliverables, each with owner, inputs and due date.
5. Missing data.
6. Decisions for the owner, CPA and counsel: trust rules, ASC 606 policy, contingent accrual method, producer classification, and book ownership.

Attach the workpapers as files.
