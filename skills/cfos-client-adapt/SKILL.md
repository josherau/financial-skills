---
name: cfos-client-adapt
description: Adapt and install the CFOS 8-step Construction Financial Operating System (CONTROL, runoncfos.com) for a specific client, including non-construction field-service businesses.
---

# CFOS client adaptation

Use this skill to take the CFOS system (CONTROL: C.F.O.S. Construction Financial Operating System, Josh Luebker, runoncfos.com) and install it at one named client. It works for trade subcontractors and GCs as written, and for field-service businesses (power washing, landscaping, HVAC service, cleaning, pest control) through the adaptation rules below.

The output is always three things:
1. **Fit assessment**: which of the 8 steps apply as written, which adapt, and which drop.
2. **Install plan**: a Claude Doc with each step's deliverable, owner, inputs and dates, built on the critical path.
3. **Adapted templates**: the client's own cost codes, equipment rates, overhead rate and pricing targets, with every number traced to client data or labelled as an estimate.

## Ground rules

- Client actuals, benchmarks and estimates stay in separate columns. Label every figure with its source and period.
- Never send client data outside the firm. If you use the original CFOS CEO Report skill, do not run its `--contribute` step. It posts client GM, OH and NP to a third party.
- Revenue recognition (percentage of completion or completed contract), tax, and lien or notice deadlines are for the client's CPA and counsel to decide. Flag them, don't decide them.
- If a number is missing, list it as missing. Never fill the gap with a plausible figure.
- Confirm the entity, its revenue band and its business model before quoting any target.

## Step 0. Intake and fit test

Collect these before building anything:

| Item | Why |
| --- | --- |
| Last 13 months P&L and balance sheet by month, from the accounting system | Overhead rate, margins, working capital, trend |
| Chart of accounts and current item/service list | Mapping to cost codes |
| AR and AP aging | 13-week cash flow |
| Equipment and vehicle list: year, make, model, replacement cost, life, maintenance, insurance, fuel | Step 02 rates |
| Payroll register by person with role (field, office, owner) | Labor burden, overhead split |
| Price list or last 20 quotes, with what the work actually cost | Step 04 gap analysis |
| Debt schedule and line of credit terms | Cash flow and lender view |
| Accounting and field software in use | Step 05 |
| Seasonality, payment terms, contract mix (one-off, recurring, contract) | Model choice |

Then classify the business model. This decides what adapts.

| Model | Examples | Unit of work | Revenue timing |
| --- | --- | --- | --- |
| A. Contract / project | Trade sub, GC, civil | Job with contract value | Progress billing, retainage, WIP |
| B. Recurring route service | Power washing, lawn care, pest, pool, janitorial | Visit / route-day | Billed per visit or monthly contract, paid in days |
| C. Demand service / T&M | HVAC or plumbing service calls, repair | Ticket / hour | Invoice at completion |

Many clients are a mix. Example: residential route work plus some commercial contracts. Run the model A rules only on the contract segment.

## The 8 steps and how each adapts

Critical path: 01, then 02, then 03, then 04. 05 can start once 01 is coded. 06 needs 04. 07 needs 03 to 06. 08 needs 03, 06 and 07. The CFOS benchmark is about 60 days to install, which only holds if 02 and 03 overlap.

### 01 Job cost structure

The rule is one cost language across estimating, accounting and field.
- Model A uses the CFOS sub format CC.SS.PP or the GC format DD-SS:III.
  - Sub categories: 01 Material, 02 Subs, 03 Equipment, 04 Small Tools, 05 Misc DJE, 06 Labor, 08 DJE, 09 General Conditions.
  - Keep part 3 = 00 unless the work is phased.
  - Every labor and equipment code carries hours.
- Model B and C keep the same cost categories, but the second level becomes the service line instead of the job phase. Example for power washing:
  - 06.10 House wash labor
  - 06.20 Roof soft-wash labor
  - 01.10 Chemicals for house wash
  - 03.10 Rig time for house wash
- In models B and C, the "job" in the accounting system is the customer or contract, or the route-day for one-off residential. Pick one and hold it.

Deliverable: a mapping sheet from the client's existing accounts and items to the new codes.

### 02 Equipment cost basis

Every machine and vehicle gets an internal rate, so it is charged to the work that used it.
- Annual cost = ownership (replacement cost ÷ life) + maintenance + insurance + other.
- Hourly rate applies to small equipment only, using Hobbs hours.
- Daily rate = annual cost ÷ actual working days after holidays, weather and downtime. Make working days an input. Do not hard-code 260.
- Monthly rate = annual cost ÷ 13. A rental month is 4 weeks, so a year has 13. Weekly rate = annual cost ÷ 52.
- Fuel and operator labor go on their own cost codes. Never bundle them into the equipment rate.
- Idle-time cost goes to overhead, not to the job.

Model B: the unit is usually the **rig**, a truck plus trailer plus pump, tank and reels, charged per route-day. That makes this step the most valuable one for route businesses.

### 03 Overhead rate

Overhead is every indirect cost, entered at the frequency it is paid and annualized. Overhead rate = annual overhead ÷ annual revenue.
- Use 8 groups:
  - office
  - software
  - administrative
  - insurance
  - non-direct employees
  - benefits and payroll tax for those employees
  - development
  - miscellaneous
- Add owned-equipment idle time as its own line.
- Owner compensation goes in overhead at market rate, even if the owner takes it as distributions.
- A PM who runs 7 or more jobs at once is overhead, not job cost.
- Model B: franchise royalties and brand-fund fees that scale with revenue are a variable cost of revenue. Keep them out of fixed overhead, or the rate overstates at low volume. Fixed franchise fees, such as tech or territory fees, are overhead.

### 04 Estimating and pricing

Price = direct cost ÷ (1 − target gross margin). Target GM = target NP + overhead rate.
- The CFOS outcome target is 22–30% GP and 12% NP.
- For construction trades with benchmarks, the benchmark rule is: NP target = max(10%, trade average + 3.5 pts), and OH target = trade average − 1 pt. This applies at revenue up to USD 25M only. State which rule set the target.
- Model B: price per service, per square foot or per visit. Build it from crew-hours × burdened labor rate, plus rig route-day rate × share of the day, plus chemicals. Compare to the current price list and show the gap per service line.

Deliverable: an estimating-to-accounting alignment, meaning the same codes in the quote as in the books.

### 05 Software and bookkeeping alignment

- Map codes into the accounting system: classes, items, or a job-cost platform.
- QuickBooks Online has no WIP, change orders or real-time budgets. Model A clients usually outgrow it, typically into Foundation, Sage Intacct or ControlQore.
- Model B usually stays on QBO plus a field-service app (Jobber, ServiceTitan, Housecall Pro). Feed visit-level revenue and labor hours by service line into QBO classes.
- Close by the 10th of the following month. Review bookkeeping weekly for 30 minutes.

### 06 Project management standards

- Model A: written PM standards, SOV front-loaded to where the work really is (never billed past what is built), a change order log, RFIs, submittals, and the stop-work, delay and nonpayment notices (counsel to check state deadlines).
- Overbilling only funds a job when overbilling % ≥ payment term ÷ job length. At 45-day terms that means 10% overbilling covers only jobs of 15+ months. Do not set a flat overbilling target.
- Model B swaps this for route and crew standards:
  - jobs per route-day;
  - quote-to-close rate;
  - re-wash and callback rate;
  - same-day invoicing;
  - deposits or card-on-file for residential;
  - net terms only on commercial contracts.

### 07 Monthly cadence

Monthly rhythm:
- Week 1: close.
- Week 2: job or service-line financials.
- Week 3: business report (P&L, balance sheet, WIP for model A).
- Week 4: 13-week cash flow.

Tools:
- **13-week cash flow** forecast plus a 24-month view.
  - The cash floor is 3–6× monthly overhead.
  - Model B uses the recurring-revenue tab for seasonal and contract billing.
- **Lender WIP**, model A only.
  - Inputs per job: contract incl. executed COs, current estimated total cost, cost to date, billed to date.
  - % complete = cost ÷ estimated cost.
  - Overbilling is a liability; underbilling is the cheapest cash to collect.
- **CEO report**: 13 months of P&L and cash.
  - Strip financing (line of credit draws, loan proceeds, owner money) out of cash collected.
  - Debt to equity: 0–1.00x is safe, over 1.00x is overleveraged.

Working capital target: 10–15% of revenue (aim 13%), with a current ratio of 1.3–2. Close the gap from retained profit and billing speed, not borrowing.

### 08 Standards and accountability

About 5 owner hours a month. Each standard has one owner and one number, reviewed in the week 3 meeting. Sample standards:
- close by the 10th;
- WIP or service-line report by the 15th;
- 13-week forecast refreshed weekly;
- overhead rate re-run quarterly;
- equipment rates re-run annually.

## Known CFOS template conflicts to flag at install

1. The 03 overhead calculator says "Healthy 9–13%". The trade benchmarks put the USD 1–5M median at about 15%.
2. Field labor burden sits in overhead in the 03 calculator. Move it into the labor rate or it is double-counted.
3. The 02 equipment template divides by 12 and uses a fixed 260 days. Use ÷13 and actual working days.
4. Three NP target rules exist: 12% flat; max(10, avg + 3.5); avg + 1.5 in the CEO report. Use one per client and say which.
5. The 13-week workbook has its own overhead tab, separate from the 03 calculator. One must feed the other. Remove the SPM + ControlQore line for firm clients.
6. The lender WIP sample rows have zero estimated cost, so they show 0% complete and 100% margin. Clear them before use.
7. The CEO report treats billing as revenue. That is not GAAP for percentage-of-completion contractors.

## Worked example: power-washing route business (model B), e.g. a Rolling Suds territory

Everything below is an estimate of structure, to be replaced with client data.
- **Service lines (01):**
  - residential house wash
  - roof soft wash
  - concrete and flatwork
  - commercial storefront and fleet
  - recurring commercial contracts
  - gutters and add-ons
- **Unit of work:** route-day per rig.
- **KPIs:** revenue per route-day.
- **Equipment (02):** truck plus trailer rig with pump, tank and reels, surface cleaners, and soft-wash system.
  - Rate per route-day on actual working days.
  - Northern territories may run 150–190 working days a year. This is an estimate; use the client's season calendar.
- **Chemicals:** sodium hypochlorite, surfactants and degreasers are material at cost per job. Track chemicals as a % of service-line revenue.
- **Overhead (03):**
  - Royalties and brand fund that scale with revenue sit above gross margin as a variable cost.
  - Owner at market wage.
  - Off-season fixed costs spread over the in-season revenue.
- **Pricing (04):** price per house size, roof square or square foot, from crew-hours plus rig share plus chemicals. Show the margin by service line against the 22–30% GP target, after the franchise variable cost.
- **Cash (07):** a seasonal 13-week forecast.
  - Pre-season: hiring, chemicals and equipment.
  - Peak: collections.
  - Off-season: the floor at 3–6× monthly overhead.
  - Recurring contracts on the recurring-revenue tab.
- **Drop:**
  - WIP, SOV and pay apps, retainage, and the lien notices.
  - Reinstate them only for commercial contract work billed on progress.
- **Benchmarks:** the CFOS trade tables have no power-washing row. Use the client's own 13-month history and franchise-system averages if the franchisor shares them. Never borrow a construction trade row.

## Install plan output

Write the plan as a Claude Doc titled "<Client> CFOS install plan". It has these sections:
1. Fit assessment: model, steps kept, adapted and dropped.
2. Baseline: the last 13 months of GM, OH, NP and working capital, from client data.
3. Targets, and the rule that set each one.
4. Step-by-step deliverables, each with owner, inputs and due date on the critical path.
5. Missing data.
6. Decisions for the owner, CPA and counsel.

Attach the adapted workbooks as files.
