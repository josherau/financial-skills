---
name: cfos-client-adapt
description: Adapt and install the CFOS 8-step Construction Financial Operating System (CONTROL, runoncfos.com) for a specific client, including non-construction field-service businesses.
---

# CFOS client adaptation

Use this skill to install the CFOS system at one named client. CFOS comes from the book CONTROL: C.F.O.S. Construction Financial Operating System by Josh Luebker and Stewart Bohrer (runoncfos.com). It works as written for trade subcontractors and GCs. It works for field-service businesses (power washing, landscaping, HVAC service, cleaning, pest control) through the adaptation rules below. The book is written for subs from USD 1M to 12M, and SPM installs it in about 60 days.

The output is always three things:
1. **Fit assessment**: which of the 8 steps apply as written, which adapt, and which drop.
2. **Install plan**: a Claude Doc with each step's deliverable, owner, inputs and dates, built on the critical path.
3. **Adapted templates**: the client's own cost codes, equipment rates, overhead rate and pricing targets, with every number traced to client data or labelled as an estimate.

The book's formula is "the system, standards, and cadence". Steps 01 to 05 are the system, 06 and 08 are the standards, and 07 is the cadence.

## Ground rules

- Keep client actuals, benchmarks and estimates in separate columns. Label every figure with its source and period.
- Never send client data outside the firm. If you use the original CFOS CEO Report skill, do not run its `--contribute` step, because it posts client GM, OH and NP to a third party.
- Revenue recognition (percentage of completion or completed contract), the tax treatment of retainage, and lien or notice deadlines are for the client's CPA and counsel. Flag them; don't decide them.
- If a number is missing, list it as missing. Never fill the gap with a plausible figure.
- Confirm the entity, its revenue band and its business model before quoting any target.
- Name the source of each target:
  - The book gives the working-capital, debt-to-equity and current-ratio targets.
  - The 12% NP and 22–30% GP outcome targets, the overbilling formula and the benchmark rule come from runoncfos.com, not the book.

## Step 0. Intake and fit test

Collect these before building anything:

| Item | Why |
| --- | --- |
| Last 13 months P&L and balance sheet by month, reconciled, from the accounting system | Overhead rate, margins, working capital, trend |
| Chart of accounts and current item/service list | Mapping to cost codes |
| AR and AP aging | 13-week cash flow |
| Equipment and vehicle list: year, make, model, replacement cost, ownership duration, maintenance, insurance and registration, major repairs, fuel | Step 02 rates |
| Payroll register by person with role (field, office, owner) | Labor burden, overhead split |
| Price list or last 20 estimates, with what the work actually cost | Step 04 gap analysis |
| Debt schedule, line of credit, any merchant cash advances | Cash flow and lender view |
| Accounting and field software in use | Step 05 |
| Seasonality, payment terms, contract mix (one-off, recurring, contract) | Model choice |
| The owner's three biggest problems this year | Step 08 standards (the book's exercise) |

Then classify the business model. This decides what adapts.

| Model | Examples | Unit of work | Revenue timing |
| --- | --- | --- | --- |
| A. Contract / project | Trade sub, GC, civil | Job with contract value | Progress billing, retainage, WIP |
| B. Recurring route service | Power washing, lawn care, pest, pool, janitorial | Visit or route-day | Billed per visit or monthly contract, paid in days |
| C. Demand service / T&M | HVAC or plumbing service calls, repair | Ticket or hour | Invoice at completion |

Many clients are a mix, for example residential route work plus some commercial contracts. Run the model A rules only on the contract segment.

## The 8 steps and how each adapts

Critical path: 01, then 02, then 03, then 04. Step 05 can start once 01 is coded. 06 needs 04, 07 needs 03 to 06, and 08 needs 03, 06 and 07. The 60-day install only holds if 02 and 03 overlap.

### 01 Job cost structure

The rule is one cost language across estimating, accounting and field.

**Three levels:**
- Level 1 is the cost category.
- Level 2 is the subcategory.
- Level 3 is the phase, area or month.

For a USD 1–12M sub, run Levels 1 and 2 on every project, and Level 3 only on phased work.

**The book's seven categories:**

| # | Category | Book rules |
| --- | --- | --- |
| 01 | Material | Level 2 by commodity. Always include a material tax code, plus a miscellaneous line for items under USD 10,000 per project. |
| 02 | Subcontractors | On-site outsourced work that needs its own COI. Level 2 by trade, plus a miscellaneous line for trades under USD 10,000. |
| 03 | Equipment | Owned, rented, trucks, fuel, fees, miscellaneous. Charged at a daily rate. |
| 04 | Tools | Large tools budgeted per project. Small tools and safety items as a lump sum of 1% of labor dollars. |
| 05 | Labor | Level 2 by work type, Level 3 by phase or month on long jobs. Budget in fully burdened dollars and track both dollars and hours against the estimate. |
| 06 | Direct job expense | PM, super, non-working foreman, job admin, safety, trailers, storage, mobilization, permits. Non-productive labor is job cost, not overhead. |
| 07 | Other | Contingency, bond, specialty insurance, project-specific interest. |

**Toolkit template numbering differs from the book:**
- Sub format CC.SS.PP: 01 Material, 02 Subs, 03 Equipment, 04 Small Tools, 05 Misc DJE, 06 Labor, 08 DJE, 09 General Conditions. It has no 07.
- GC format DD-SS:III.
- Use the template numbering, since it is the file the client builds from, and record the choice in the install plan.

**Coding rules:**
- Keep part 3 = 00 unless the work is phased.
- Every labor and equipment code carries hours.

**Models B and C** keep the same cost categories, but the second level becomes the service line instead of the job phase. Example for power washing:
- 06.10 House wash labor
- 06.20 Roof soft-wash labor
- 01.10 Chemicals for house wash
- 03.10 Rig time for house wash

In models B and C, the "job" in the accounting system is the customer or contract, or the route-day for one-off residential work. Pick one and hold it.

**Documentation standard:** costs must be provable to a judge or arbitrator, including owned equipment by the day. In the book, a USD 240,000 equipment-standby claim was denied because owned equipment had never been job costed.

**Deliverable:** a mapping sheet from the client's existing accounts and items to the new codes. The book has no separate mapping template; the cost-code template plus the step 04 alignment meetings produce it.

### 02 Equipment cost basis

Every machine and vehicle gets an internal rate, so its cost is charged to the work that used it.

**Inputs:**
- ownership duration;
- replacement cost, for the right-sized machine;
- annual maintenance;
- insurance and registration;
- major repairs;
- annual working days.

**Rates:**
- Annual cost = ownership (replacement cost ÷ ownership years) + maintenance + insurance and registration + major repairs spread over the ownership years.
- Daily rate = annual cost ÷ actual working days. This is the rate used in job costing.
- Working days start from the 260-day default (5 × 52), less holidays, weather and planned downtime. Make working days an input.
- Monthly rate = annual cost ÷ 13, because a rental month is 4 weeks and a year has 13 of them. Weekly rate = annual cost ÷ 52.
- Use hourly rates only in special cases. The book's example is lawn equipment that serves 5–10 jobs a day.

**What stays out of the rate:**
- Fuel, operator labor and mobilization go on their own cost codes. Never bundle them into the equipment rate.
- Idle-time cost goes to overhead, not to the job.

**Book example:** an excavator day costs USD 799 = 375 machine + 144 fuel (6 gal/h × 6 h × USD 4/gal) + 280 operator (8 h × USD 35 burdened). The owner was billing it at USD 800, so his price was his cost.

**Model B:** the unit is usually the **rig** (truck, trailer, pump, tank and reels), charged per route-day. Small equipment that moves across many stops a day can use the book's hourly exception. That makes this step the most valuable one for route businesses.

### 03 Overhead rate

Overhead is every expense it takes to keep the business open when you are not building.

**The book's 8 categories:**
1. office requirements;
2. software subscriptions;
3. administrative expenses;
4. employee benefits and development, including marketing (field-staff benefits go to job cost);
5. owned-equipment idle time and normal maintenance;
6. insurance;
7. non-direct job employees, including the owner;
8. miscellaneous.

The toolkit calculator has 7 groups, so map them to the book's 8.

**Two methods:**
- *Starter*, before job costing works: annualize each expense at the frequency it is paid, then divide by annual revenue.
- *Exact*, once job costing works: total expense / SG&A for the last 12 reconciled months ÷ revenue for the same months. Re-run it monthly after the bank reconciliation as a rolling 12-month figure.

**Allocation rules:**
- Owner compensation goes in overhead at market rate, even if it is taken as distributions.
- A PM who floats across 7 or more projects, or does company-wide work, is overhead. A PM dedicated to a few jobs is job-costed.
- Workers' comp: field workers' comp goes in the labor burden, office workers' comp in overhead. The book lists it in both places, so write the split down.
- Run the calculator's scenario mode at full utilization and in a slowdown.

**Model B:** franchise royalties and brand-fund fees that scale with revenue are a variable cost of revenue. Keep them out of fixed overhead, or the rate overstates at low volume. Fixed franchise fees, such as tech or territory fees, are overhead.

### 04 Estimating and pricing

**Pricing formula:** price = direct cost ÷ (1 − target gross margin), where target GM = target NP + overhead rate.

**Targets:**
- The site's outcome targets are 22–30% GP and 12% NP.
- For construction trades with benchmarks, the site's benchmark rule is NP target = max(10%, trade average + 3.5 pts) and OH target = trade average − 1 pt, at revenue up to USD 25M only.
- State which rule set the target.

**Alignment meetings (book):**
- Four one-hour meetings over four weeks, first thing in the morning.
- Attendees: estimators, PMs, supers, CFO, ops manager, controller and bookkeepers.
- Walk a past estimate line by line against the codes. Start with the easy costs, then the contested ones: safety glasses, ladders, store runs, small labor task switches.
- Agreement matters more than being right.
- Do this before the next bid.

**What estimates usually miss (book):** financing costs, small tools, PM and super time, and on-site storage. If any of these is labelled "markup", it is missing.

**Model B:** price per service, per square foot or per visit. Build the price from:
- crew-hours × burdened labor rate;
- plus the rig's route-day rate × its share of the day;
- plus chemicals.

Compare the result to the current price list and show the gap per service line.

**Deliverable:** an estimating-to-accounting alignment, meaning the same codes in the quote as in the books.

### 05 Software and bookkeeping alignment

**The book's test:** can the PM pull up line-by-line spend against the estimate in 30 seconds, without asking accounting? The book supplies no template for this step; the test is the deliverable.

**Fix the book's three bookkeeping errors first:**
1. Equipment expensed instead of capitalized. Cleanup costs USD 5,000–12,000.
2. Retention not split out and billed separately. The book says it then gets taxed as revenue before collection. Treatment depends on the client's accounting and tax method, so the CPA decides.
3. Labor booked to SG&A instead of COGS, or hourly pay booked to COGS while the burden sits in overhead.

**Software:**
- Map codes into the accounting system: classes, items, or a job-cost platform.
- Model A: QuickBooks Online has no WIP, change orders or real-time budgets, so these clients usually outgrow it, typically into Foundation, Sage Intacct or ControlQore.
- Model B usually stays on QBO plus a field-service app (Jobber, ServiceTitan, Housecall Pro). Feed visit-level revenue and labor hours by service line into QBO classes.

**Rhythm:** PMs approve costs weekly, and the books close by the 10th of the following month.

### 06 Project management standards

**The book's six standards to write down:**
1. the billing date;
2. how contracts are negotiated;
3. when a notice of nonpayment is sent, and by whom;
4. when delay notices are sent, and how the GC conversation goes;
5. what escalates to ownership;
6. when change orders are sent.

The toolkit's PM standards document has 19.

**The book's defaults:**
- bill on the 15th;
- issue a change order for every change of conditions, without exception;
- send the notice of nonpayment on day 40 after the GC sent its pay app to the owner;
- the PM sends anything under USD 80,000 without owner approval.

Counsel checks state notice deadlines.

**Model A also needs:**
- an SOV front-loaded to where the work really is, never billed past what is built;
- a change order log;
- RFIs and submittals;
- stop-work, delay and nonpayment notices.

**Overbilling (site rule):** overbilling only funds a job when overbilling % ≥ payment term ÷ job length. At 45-day terms, 10% overbilling covers only jobs of 15+ months. Do not set a flat overbilling target.

**Model B swaps this for route and crew standards:**
- jobs per route-day;
- quote-to-close rate;
- re-wash and callback rate;
- same-day invoicing;
- deposits or card-on-file for residential;
- net terms only on commercial contracts.

### 07 Monthly cadence

The order of the month (book):

| When | What |
| --- | --- |
| Weekly | Bookkeeping, with PM cost approvals |
| By the 10th | Close and bank reconciliations for the prior month |
| First Monday after the 10th | Cost-to-complete meeting: each project gives % complete per task and dollars left per line, and PMs present to leadership |
| After the cost-to-complete | CEO report |
| Last week of the month | Cash flow forecast (weekly when cash is tight) |

**Cost-to-complete red flags.** For each line trending over, ask:
- Are we missing a change order?
- Did we underestimate?
- Do the specs not work?
- Does the build strategy need adjusting?

Correct repeatable work (floors, phases) before the next unit.

**CEO report**, rolling 12 months:
- **Revenue** counts only invoices committed in the accounting system for the month. Draft invoices, T&M tickets, change orders not fully approved, and retention not expected for years are excluded.
- **Active cash flow** = payments received − expenses paid. It shows seasonal burn.
- **Gross margin and net margin.**
- **Overhead** as a rolling 12-month %, fed back into estimates monthly.
- **Diagnostics:**
  - If GM is at or above the industry average and net margin is low, overhead is the problem.
  - Three months of losses or shrinking revenue means cutting overhead to match.
- Strip financing (line of credit draws, loan proceeds, owner money) out of cash collected.

**Balance sheet (book):**
- **Working capital** = current assets − current liabilities. Target 10–15% of annual revenue; the CEO report uses 13%.
- **Debt to equity** = total liabilities ÷ total equity.
  - 0–1 is safe, and closer to 0 is better.
  - Over 1 is overleveraged.
  - Negative equity is a red flag.
- **Current ratio** = current assets ÷ current liabilities. Target 1.3–2.
  - Below 1 is a red flag.
  - Above 2 leaves room for distributions as long as it stays above 1.3.
- Close any working-capital gap from retained profit and billing speed, not borrowing.

**Lender WIP**, model A only:
- **Inputs per job:** name, contract price, estimated total cost, cost to date, billed to date.
- **Contract price** includes **fully executed** change orders only.
- **Estimated total cost** is **re-estimated monthly** as cost to date + cost to complete, not the bid. For example, a sub bought out below budget shows at the buyout figure.
- **% complete** = cost to date ÷ estimated total cost.
- **Over and under billing:** overbilling is a liability. Underbilling is an asset, and it is the cheapest cash to collect.
- **Accuracy target:** 98%.

**13-week cash flow** forecast plus the 24-month view:
- Ask four questions: what are we expecting, how much do we need, can we survive without it, and which invoices must we collect?
- Start with a 6–8 week first forecast.
- The cash floor is 3–6× monthly overhead.
- Test decisions before making them: bonus timing, overtime levels, equipment purchases.
- Model B uses the recurring-revenue tab for seasonal and contract billing.

### 08 Standards and accountability

**Owner time (book):** about 5 hours a month.
- 30 minutes a week reviewing bookkeeping.
- 3 hours a month on job costing, metrics and the cash forecast.

**How standards work:**
- Each standard has one owner and one number.
- Review them after the cost-to-complete meeting.
- Standards stay non-negotiable when busy.

**Start with the book's exercise.** List the three biggest problems this year, then the action that would have prevented each one. Turn each action into a standard.

**Sample standards:**
- close by the 10th;
- cost-to-complete by the first Monday after the 10th;
- 13-week forecast refreshed weekly when cash is tight;
- overhead rate re-run monthly on the rolling 12 months;
- equipment rates re-run annually.

## Known CFOS template conflicts to flag at install

1. **Overhead benchmark.** The 03 overhead calculator says "Healthy 9–13%". The book says most subs run 25–42%, and its cleaned-up cases land at 13–18%. The trade benchmarks put the USD 1–5M median at about 15%.
2. **Labor burden.** The 03 calculator puts field labor burden in overhead. Move it into the labor rate, or it is double-counted. The book (Ch5) calls this split an error.
3. **Equipment divisors.** The 02 equipment template divides by 12 and uses 260 days. Use ÷13 for monthly rates, and subtract holidays and downtime from the 260-day default.
4. **NP target.** Three rules exist: 12% flat; max(10, avg + 3.5); and avg + 1.5 in the CEO report. Use one per client and say which.
5. **Duplicate overhead tab.** The 13-week workbook has its own overhead tab, separate from the 03 calculator. One must feed the other. Remove the SPM + ControlQore line for firm clients.
6. **WIP sample rows.** The lender WIP sample rows have zero estimated cost, so they show 0% complete and 100% margin. Clear them before use.
7. **Revenue definition.** The CEO report, and the book, count invoiced revenue. That is not GAAP for percentage-of-completion contractors, so it won't match reviewed or audited statements.
8. **Cost category numbering.** The book numbers the categories 01–07 (05 Labor, 06 DJE, 07 Other). The sub template uses 05 Misc DJE, 06 Labor, 08 DJE and 09 General Conditions. Pick one per client.
9. **Overhead categories.** The book has 8 overhead categories (benefits and development combined, idle time included). The calculator has 7.
10. **Workers' comp.** Ch1 puts it in the labor burden, and Ch3 lists it under overhead insurance. Split field from office.
11. **Retention tax claim.** The book says retention that isn't billed separately gets taxed as revenue. That is a CPA question, not a rule.

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
- **KPI:** revenue per route-day.
- **Equipment (02):** a truck-and-trailer rig (pump, tank, reels), surface cleaners, and a soft-wash system.
  - Rate per route-day, on actual working days.
  - Northern territories may run 150–190 working days a year (estimate; use the client's season calendar).
  - Surface cleaners and other small units moved across many stops a day can use the hourly exception.
- **Chemicals:** sodium hypochlorite, surfactants and degreasers are material at cost per job. Track chemicals as a % of service-line revenue.
- **Overhead (03):**
  - Royalties and brand fund that scale with revenue sit above gross margin as a variable cost.
  - Owner at market wage.
  - Spread off-season fixed costs over in-season revenue, using the exact rolling 12-month method.
- **Pricing (04):** price per house size, roof square or square foot, built from crew-hours plus rig share plus chemicals. Show the margin by service line against the 22–30% GP target, after the franchise variable cost.
- **Cash (07):** a seasonal 13-week forecast.
  - Pre-season: hiring, chemicals and equipment.
  - Peak: collections.
  - Off-season: hold the floor at 3–6× monthly overhead.
  - Recurring contracts go on the recurring-revenue tab.
  - Active cash flow by month shows the off-season burn.
- **Drop:** WIP, SOV and pay apps, retainage, and the lien notices. Reinstate them only for commercial contract work billed on progress.
- **Benchmarks:** the CFOS trade tables have no power-washing row. Use the client's own 13-month history, plus franchise-system averages if the franchisor shares them. Never borrow a construction trade row.

## Install plan output

Write the plan as a Claude Doc titled "<Client> CFOS install plan", with these sections:
1. Fit assessment: model, steps kept, adapted and dropped, and the cost-code numbering chosen.
2. Baseline: from client data, the last 13 months of:
   - GM, OH and NP;
   - active cash flow;
   - working capital, debt to equity and current ratio.
3. Targets, with the rule and the source that set each one.
4. Step-by-step deliverables: each with owner, inputs and due date on the critical path, ending with the first cost-to-complete meeting and the first 6–8 week forecast.
5. Missing data.
6. Decisions for the owner, CPA and counsel.

Attach the adapted workbooks as files.
