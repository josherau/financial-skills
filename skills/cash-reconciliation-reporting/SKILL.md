---
name: cash-reconciliation-reporting
description: Use this skill to run a finance-grade cash reconciliation workflow. It begins with a mandatory sweep of every live connected system — ledger, AR, AP, card and expense platforms — before any file is opened, normalizes transactions, reconciles bank to ERP by entity/account and consolidated, asks concise multiple-choice clarification questions when assumptions materially affect the output, uses visual diagnostic reasoning, flags exceptions, requires every cause to be researched rather than asserted and every flagged anomaly to be investigated in the same pass, runs a mandatory adversarial pre-ship audit pass that attacks conclusions rather than only checking arithmetic, and produces a CFO-ready reconciliation pack with dashboard-ready data and grounded executive summary.
---

# Cash Reconciliation & Reporting Skill

## Purpose

Use this skill to turn cash-related source data into a controlled cash reconciliation pack. The goal is to validate cash movement before creating commentary or dashboard output.

The workflow supports weekly or period-end cash reconciliation using live ERP connections, bank statements, AR and AP subledgers, card platforms, prior cash reports, and supporting files.

This skill must be generic and reusable across companies. Do not hardcode company names, bank names, sample data, email addresses, categories, or file names.

## Core workflow

Run the workflow in this order:

0. **Run the live-source discovery sweep. Do not open a single file until it is done.**
1. Inspect inputs and create an input log.
2. Normalize bank and cash transaction data.
3. Reconcile cash by entity/account and consolidated.
4. Flag exceptions, explain supported cash drivers, and produce the reconciliation pack.
5. **Run the adversarial pre-ship audit pass. Do not deliver until it passes.**

Do not start with the dashboard. Build the controlled reconciliation layer first.

---

## STEP 0 — Live-source discovery sweep — MANDATORY

**Every reconciliation begins by exhausting the live connected systems.** Not the ledger alone — every system that holds cash-relevant data. A pack built before this sweep is incomplete by construction, and the gaps surface later as questions the reader has to send back.

This step exists because the recurring failure is not arithmetic. It is **shipping a pack with a hole in it, labelling the hole "not available", and being wrong about that.**

### Enumerate what you can reach

Before anything else, list every connected system available in the session and decide, in writing, whether each holds cash-relevant data:

- ERP / general ledger
- AR subledger — open invoices, customers, due dates, payment status
- AP subledger — open bills, vendors, due dates, payment status
- Card and expense platforms
- Payment processors, bill-pay and treasury platforms
- Payroll systems
- Banking connectors

Record the result in a **`Source_Sweep`** tab: system, queried yes/no, object or endpoint used, filter applied, rows returned, and what it was used for. If a system was not queried, the tab must say why. An empty cell is not an answer.

### AR and AP are NOT optional

**Query the AR subledger and the AP subledger on every single run**, whether or not the requester mentioned them, and whether or not a prior period's pack omitted them.

They are mandatory because cash cannot be interpreted without them:
- Bank cash tells you what happened. AR and AP tell you what is *about* to happen.
- No liquidity, runway or working-capital statement is supportable without both.
- An unpaid receivable that should have been collected is a finding in its own right.
- Open payables at period end change the meaning of a healthy closing balance.

If AR or AP genuinely cannot be reached after the tests below, that is a **High-severity exception**, not a footnote — a data gap that blocks a material conclusion is High regardless of dollar amount.

### Subledger headers often cannot be filtered by entity — the lines can

This is the single most common false "unavailable" in this workflow.

In many ERPs the AR/AP **header** object carries no entity, location or department dimension at all. Filtering on it is **silently ignored** and returns the whole shared ledger across every entity, which looks like unusable data and invites the wrong conclusion.

The dimension lives on the **line/detail** object. Before concluding anything:

1. **Inspect the object's field list.** Confirm whether the dimension field actually exists on that object. Do not infer it from a failed query.
2. **Try the line-level object** (invoice *items*, bill *items*, transaction *details*). Filter the dimension there.
3. **Try the control account.** Period-end GL balances for the AR and AP control accounts give you the totals even when the subledger is awkward, and they double as a tie-out.
4. **Try a different object family** — aging objects, summary objects, saved reports.

Join line back to header (line record-key = header record-number) to get due dates and payment dates.

### "Not obtainable" is a claim that must itself be tested

Never write "not available" until you have tried the control account, the line-level object, and a different object family, and can name each attempt. **One object failing is not the data being unavailable.**

When a limitation does survive, state the **narrow** one that is actually true — not the broad one that is convenient. "A point-in-time days-past-due aging is not available because line-level paid amounts are as-at-today" is a real limitation. "AR is not available" would have been false.

### Point-in-time versus as-at-today

Subledger line-level "paid" fields usually reflect status **now**, not at the period end. An invoice paid after period end was **open** at period end.

- For a true point-in-time aging, join to the header for the payment date.
- If you present a current-status view instead, **label it explicitly** as "still unpaid as at <date>" and never call it an aging.

### Never overstate the test window

Before claiming an item was tested through a date, **confirm the ledger actually holds entries through that date.** Query the maximum entry date. Claiming a test window that runs past the last populated period is false assurance — it converts "we have no data" into "we checked and found nothing."

State the real window: "searched all accounts through <last populated date>."

### Disputed, contested and non-standard receivables

Some receivables are not going to behave like receivables. Claims in dispute, certified claims, contested billings, items in litigation or appeal, and balances subject to a pending settlement all fall here.

When the requester tells you an item is of this kind, or the data shows a long-dated balance with no collection activity:

- **Carry it on its own line**, named for what it is, never inside a current aging bucket.
- **Never let it feed** a DSO, collection-timing, liquidity or runway figure. Exclude it and **say that you have excluded it.**
- Age it in months from origination and label collectability as **not assumed**.
- Once the requester has confirmed the status, **do not re-raise it as a new exception every period.** Park it, carry it forward, restate the age, and report only a *change* in status. Re-flagging a known accepted position as a fresh finding wastes the reader's attention and buries the things that are actually new.

### Carry forward what earlier runs established

Where prior findings, standing decisions or source-system quirks have been recorded, read them before starting and apply them. Re-deriving a known answer wastes a cycle; contradicting a standing decision without saying so is worse. Where this run's evidence overturns something previously recorded, **say so explicitly** and correct the record.

---

## Input inspection

Inspect all supplied files before calculating. Identify each file's likely role based on structure and content, not file name alone.

Classify files where possible as:

- Bank statement or bank transaction export
- ERP cash GL export
- AR aging or open receivables export
- AP aging or open payables export
- Prior cash report or prior reconciliation
- Category mapping or account mapping
- Other supporting source

Create an Input_Log with:

- Source file name
- Source type
- Reporting period detected
- Entities or bank accounts detected
- Key columns found
- Row count
- Currency if available
- Any parsing or completeness issues

If a file cannot be classified confidently, keep it in the input log and ask a clarification question if it materially affects the reconciliation.

**A file is never a substitute for a live system that can answer the same question.** Where a file is used because a live system genuinely cannot reach the data, label it as such in the deliverable. Where a workpaper is tested, it belongs in a comparison tab, never as an input — a workpaper is evidence of what someone concluded, not evidence of what the ledger says.

### Account discovery — do this before trusting any account list

A reconciliation is only as complete as the account population behind it. Before reconciling:

- Enumerate the chart of accounts from the **live system**, not only from an exported file. Exports go stale and routinely omit system-generated accounts.
- Query account codes across **both numeric and alphanumeric ranges**. Integration-created accounts (card programs, payment processors, clearing accounts) frequently use alphabetic or mixed codes and are invisible to a purely numeric range query.
- Where the system supports an account category or class, query that too — it is usually the most reliable completeness test.
- Reconcile the account list to the list of real-world bank and card accounts. Any bank or card account with no ledger account is a **Critical** finding, regardless of its balance.
- Never state that a category of balance is nil until you have searched the full account population for it.

---

## Multiple-choice clarification rules

Ask concise multiple-choice questions when an assumption materially changes the reconciliation, exception treatment, categorization, or output.

Use multiple-choice questions instead of broad open questions whenever practical.

Each question should have:

- One clear decision to make
- Three to five answer choices labeled A, B, C, D, and optionally E
- A recommended default choice when finance practice strongly supports one
- A short explanation of why the question matters

Ask questions before finalizing affected outputs, not after.

Do not ask questions for low-impact formatting preferences. Make a reasonable assumption and document it.

Areas where multiple-choice clarification is appropriate:

- Source of truth for actual cash
- Treatment of bank-only items
- Treatment of ERP-only items
- Duplicate candidate handling
- Timing difference handling
- Sign convention conflicts
- Entity or account mapping ambiguity
- Unmapped transaction category treatment
- Materiality threshold for exceptions
- Whether to create adjusted totals or only reported totals
- Treatment of disputed or contested receivables

If the user does not answer, proceed with conservative finance assumptions, document the assumptions, and keep the affected items in the exception log.

## Normalization requirements

Create a normalized transaction table before reconciling.

Required normalized fields:

- transaction_date
- value_date, if available
- entity
- bank_account or cash_account
- source_system
- source_file
- transaction_reference
- description
- counterparty, if available or inferable
- original_amount
- currency
- inflow
- outflow
- net_amount
- category
- category_confidence
- match_status
- notes

Normalization rules:

- Standardize dates.
- Preserve original descriptions.
- Preserve source file traceability.
- Convert debit/credit or positive/negative formats into inflow, outflow, and net_amount.
- Do not overwrite source data.
- Do not net transactions together unless explicitly required for a summary view.
- Assign categories using available mapping, account codes, descriptions, and counterparties.
- Use confidence scores or confidence labels for inferred categories.
- Leave low-confidence classifications visible instead of hiding them in broad categories.

## Reconciliation requirements

Reconcile cash in a controlled sequence:

1. By entity.
2. By bank account or cash account.
3. Consolidated.

For each entity/account, calculate:

- Opening cash
- Total inflows
- Total outflows
- Net cash movement
- Expected ending cash
- Reported ending cash, if available
- Difference
- Difference explanation status

Use this equation as the primary control:

Opening cash + inflows - outflows = ending cash

**Always start from the BOOK opening balance, not the bank opening balance.** A reconciliation that opens from the bank figure cannot detect a carryforward — it will match every line in the period and still report a zero difference while concealing a material prior-period gap. Reconcile every account, not only the busy one.

Then compare bank cash movement to ERP cash GL movement where ERP data is available. **Pull the GL with no journal-type filter.** A GL export limited to selected journals silently omits other receipts, quick payments and general journal entries, and will produce a confidently wrong closing balance.

Identify and separate:

- Bank items missing in ERP
- ERP items missing in bank
- Duplicate candidate transactions
- Timing differences
- Sign issues
- Entity mapping issues
- Currency issues
- Unexplained differences
- Open AR/AP items that conflict with observed cash activity

Always reconcile entity-level differences before consolidated totals.

Never conclude that cash reconciles simply because the consolidated difference is small. If entity-level differences offset each other, flag this as a high-risk issue — and never quote one account's difference in isolation when accounts run in opposite directions.

### Aggregate before declaring a mismatch

Ledgers routinely post as components what the bank presents as one figure — payroll gross versus its direct-deposit, tax and fee legs; one vendor payment against several bill lines. A naive line-by-line match reports these as unmatched on both sides.

Before listing anything as a difference, test whether a group of ledger lines sums to a single bank line, and vice versa. **Disclose the match basis** for every non-obvious match in the pack.

### Timing differences must be proven, never assumed

**"Timing difference" is a conclusion, not a label of convenience.** It asserts that an item will resolve itself in a later period. If that assertion is wrong, the item is an *unrecorded transaction* — cash has moved with no ledger record — and the reader has been told to wait for something that will never happen.

Before describing any item as a timing difference:

- **Find it in a later period.** Query the ledger for the specific amount across the following periods, up to the last date the ledger is actually populated. If later-period data does not yet exist, label it `timing — unproven` and say so.
- **Beware the recurring-amount trap.** A fixed monthly charge — a subscription, a service fee, a standing bank charge — will appear in later periods at the identical amount. That later hit is *that month's own charge*, not proof the item under test ever posted. Match on identity (description, period, reference, vendor), not on amount alone. Matching a recurring amount and calling it proven is a false positive that a purely arithmetic check will never catch.
- **Search the whole ledger, not just the cash account.** An item may post to a liability, clearing or suspense account while the cash leg is never recorded. That is a *half-posted entry*, not a timing difference, and the un-relieved balance is the control total to report.
- **Classify every reconciling item into one of three buckets**, and total them separately:
  1. `Timing — proven` — found in a later period, on identity.
  2. `Timing — unproven` — later data not yet available, or identity could not be established.
  3. `Unrecorded` — searched later periods and the full account population; not present. **This is a Critical finding.**
- **Recurring items deserve extra suspicion.** An item that appears as a reconciling difference in two or more consecutive periods is almost certainly unrecorded rather than timing. Test it explicitly.

Never write a root-cause narrative that attributes the whole difference to a posting lag until every item has been bucketed.

### Carryforward balances must be itemized and aged

Never carry a prior-period difference into the current pack as a single opaque number.

- Show an aged listing of open reconciling items, oldest first, with the period each arose.
- Reconcile the prior period's closing difference to the current period's opening carryforward, and show that it agrees.
- Age buckets (current period / 1 period old / 2+ periods old) belong in the pack. Anything 2+ periods old should be presumed unrecorded until proven otherwise.
- Where intervening periods were never reconciled, **say so plainly**, age the gap by month from balances, and state that item-level aging is not possible. Do not present a monthly split as though it were item-level evidence.

## Visual diagnostic reasoning

Use visual reasoning during the workflow before finalizing the pack. These visuals are diagnostic checks, not the final dashboard.

Create compact in-chat charts, visual summaries, or chart-ready tables when they help inspect:

- Opening cash to ending cash bridge
- Bank vs ERP differences by entity/account
- Top cash inflows and outflows
- Exception amount by severity
- AR and AP near-term cash pressure
- Category-level cash movement
- Aging of open reconciling items

Keep diagnostic visuals simple and decision-oriented. Use them to find issues, not to decorate the output.

When a visual reveals a possible issue, write the issue into the Exception_Log and tie it back to the source data.

## Exception log requirements

Create an Exception_Log even if no exceptions are found.

Required fields:

- exception_id
- severity
- exception_type
- entity
- account
- amount
- source_file
- source_reference
- description
- likely_cause
- recommended_follow_up
- status

Severity guidance:

- High: Material difference, unexplained cash movement, duplicate affecting cash, missing ERP posting, unrecorded transaction, unmapped bank or card account, entity-level issue hidden by consolidation, liquidity constraint, missing AR or AP data, or item requiring CFO attention.
- Medium: Classification uncertainty, likely timing difference, incomplete source detail, or open AR/AP conflict.
- Low: Formatting issue, minor missing field, or non-material data quality issue.

### Grade severity mechanically, not by judgement

State the materiality rule explicitly in the pack, then **enforce it in code** — iterate the exception rows, compute the expected severity, and compare to the assigned severity. Report any mismatch as an audit finding and fix it before shipping.

Escalating categories override the amount test. An item that is a control failure, an account-mapping gap, an unrecorded transaction, a liquidity constraint, or a data gap that blocks a material conclusion is High **regardless of its dollar amount** — including when that amount is zero or trivially small. Zero-amount findings sort to the bottom of an amount-ordered list, which is exactly how the most important items get overlooked.

Do not bury exceptions in commentary. Keep them visible and traceable.

**Do not re-raise accepted positions as new findings.** Where a matter has been confirmed by the requester as known and accepted, carry it as a standing item with its age restated, and report only changes.

## Cash driver commentary

Write commentary only after the reconciliation and exception log are complete.

Separate:

- Facts directly supported by source data
- Assumptions used
- Interpretation or commentary
- Follow-up questions

Every driver comment must tie to a transaction, category, entity, account, AR/AP item, or reconciliation result.

Do not invent explanations. If the source data does not support a conclusion, say so and list the follow-up needed.

The commentary should answer:

- What drove cash inflows?
- What drove cash outflows?
- Which entity/account drove the movement?
- What changed versus available history?
- **How much of the inflow was operating versus funding, related-party or non-recurring?** State the closing position excluding non-operating funding.
- What exceptions require review?
- **What cash risks are visible from AR and AP?** — answered from the live subledgers, with disputed items excluded and that exclusion stated.
- What cannot be concluded from the available data?

## Output pack requirements

When file creation is available, create a workbook named with a clear cash reconciliation pack title and reporting date.

Recommended tabs:

- README
- Source_Sweep
- Input_Log
- Bank_Normalized
- ERP_Cash_GL
- Bank_vs_ERP_Reconciliation
- Open_Items_Aging
- Item_Buckets
- AR_Aging_Summary
- AP_Aging_Summary
- Exception_Log
- Cash_Drivers
- Dashboard_Data
- Executive_Summary
- Audit_Log

The workbook should be suitable as the controlled input for a separate CFO dashboard skill.

The Dashboard_Data tab should include clean, aggregated tables that a dashboard can use without redoing the reconciliation.

The Executive_Summary tab should include:

- Reporting period
- Ending cash
- Net cash movement
- Major inflow drivers, split between operating and funding/related-party
- Major outflow drivers
- Reconciliation status
- Split of reconciling items between proven timing, unproven timing and unrecorded
- AR and AP position, with disputed items shown separately
- High-severity exceptions
- Recommended CFO follow-ups

The Audit_Log tab records the pre-ship audit pass: what was tested, what passed, what failed, and what was corrected.

**Rebuild the workbook from a script, never by hand-editing the output.** Keep the build script so the pack can be regenerated and re-audited. Where the deliverable already exists, update it in place rather than creating parallel versioned copies.

---

## Never state an unresearched cause. Never just flag. — MANDATORY

Two failures that arithmetic verification will never catch, both observed in real packs.

### A cause is a claim, carrying the same burden of evidence as a number

Do not write **"because", "driven by", "attributable to", "consists of", "reflects"** or **"so an exact tie is not expected"** unless you have queried the thing and can name the documents behind it.

A worked example. A pack disclosed an AP-to-GL difference as *"GL 20000 also carries credit memos, manual journals and reclassifications that are not open AP bills."* Nobody had looked. On testing, **every** bill line offset to the AP control account — there was no classification leakage at all, and the real cause was a sub-ledger-to-general-ledger posting lag. The guess was not merely unproven; it was wrong, and it pointed the reader at the wrong remediation.

Note what made it slip through: the sentence was wrapped in honest-looking framing — *"disclosed, not explained"* — and a fabricated cause was smuggled inside it. **Hedging does not lower the bar.** "Likely", "typically", "would be expected to", "disclosed" — none of these license an unresearched cause.

If a cause genuinely cannot be established, state only what was tested:

> Correct: *"$X unexplained. Tested A, B and C; the cause is not established."*
> Wrong: *"$X unexplained, probably Y."*

And when components are pinned but do not sum to the difference, **say the decomposition does not close.** Do not let a partial attribution imply a full one.

### Noticing an anomaly is not a finished unit of work

**Never park a flag.** "Requires investigation", "not investigated", "to be confirmed", "worth a look", "separate issue" are **not acceptable as an end state** in a shipped pack. If you can see it, investigate it in the same pass.

A worked example. A pack raised an abnormal **debit balance in the AP control account** and left it as *"separate issue, still uninvestigated."* Resolving it took **two queries**: the balance object re-run **with dimension fields** identified the vendor and department; a detail query filtered on that vendor exposed the history. The answer was that two invoices had been relieved **three times on one day** — paid from the operating bank, paid again from a card-programme bank, and the underlying bills reversed — over-relieving by roughly twice the invoices' value. A parked flag was concealing a genuine double-payment control failure worth far more than the residual balance suggested.

**Most anomalies in a ledger are two queries deep.** The reusable pattern:

1. Re-run the **control-balance query with every dimension field** (vendor, department, project, customer, employee). A net-nil vendor can hide equal and opposite department balances; the abnormal row identifies itself once dimensions are exposed.
2. Query the **transaction detail filtered on that dimension** for the full history. The batch/source-module label on each entry usually exposes the mechanism immediately — duplicate relief, wrong-module posting, reversal without re-raise.

The bar for leaving anything open is high. Only leave it if you actually tried and hit a wall, and then say precisely what you ran, what it returned, and what specific access would close it:

> Correct: *"Queried the control balance by dimension and the detail by vendor; both return X. Closing this needs the card statement, which is not in any connected system."*
> Wrong: *"Requires investigation."*

An exception may state what the follow-up **action** is — post the entry, chase the customer, confirm with the counterparty. It may not use "investigate" as a substitute for having done the work.

## Pre-ship audit pass — MANDATORY AND ADVERSARIAL

**Arithmetic checks are not verification.** Recalculation, footing and tie-out checks prove only that the maths is internally consistent. A pack in which every figure foots and every bridge closes to zero can still carry a wrong conclusion, and has.

**The auditor's job is to break the pack, not to bless it.** Approach every check assuming the pack is wrong and you are looking for the reason. A check run in a confirming frame finds nothing. Every check below must be run, and the results recorded on the Audit_Log tab, before the pack is delivered.

### Tier 1 — Mechanical (automate in code)

| Check | Test |
|---|---|
| Formula integrity | No error values; recalculate the workbook and confirm zero errors |
| Hardcoded values in formulas | Denominators and drivers reference cells, not literals |
| Cross-tab agreement | Every figure appearing on more than one tab agrees to the cent |
| Bridge closure | Each account bridge reconciles book to bank exactly |
| Roll-forward | Opening + movement = closing, per account and consolidated |
| Sign convention | Inflows and outflows are not reversed |
| Severity conformance | Assigned severity matches the stated materiality rule for every row |
| Completeness | Every bank line is matched to a ledger line or listed as a reconciling item; no line is silently dropped |
| Source sweep complete | Every connected system appears on Source_Sweep with a queried/not-queried answer and a reason |

### Tier 2 — Assertion testing (the checks that catch wrong conclusions)

Run this tier **twice**, and on the second pass deliberately try to falsify what the first pass concluded.

| Assertion made in the pack | How to test it |
|---|---|
| "This is a timing difference" | Find the item in a later period **by identity, not amount**. If absent from the entire ledger, it is unrecorded — reclassify and escalate |
| "This recurring charge posted later" | Confirm the later hit is the *same* charge and not the following month's. Default to unproven |
| "Tested through <date>" | Confirm the ledger holds entries through that date. Never claim a window past the last populated period |
| "This balance is nil" | Search the full account population, numeric and alphanumeric and by category, before asserting nil |
| "These accounts are the complete population" | Reconcile the ledger account list to the real-world bank and card account list |
| "AR / AP is not available" | Prove you tried the line-level object, the control account, and a second object family. Name each attempt |
| "This is the AR aging" | Confirm it is point-in-time, not as-at-today status. If as-at-today, relabel |
| "This is the prior-period carryforward" | Itemize it and age it; confirm it agrees to the prior pack's closing difference |
| "This item matched" | Confirm the match basis (amount, date, reference, aggregation) and disclose it |
| "Cash improved" | Strip out funding, related-party and non-recurring inflows and re-state |
| "Nothing else is outstanding" | Re-run the completeness check from the source side, not the workbook side |
| "This difference is caused by <X>" | **Causal sweep.** Name the query that proved it. If none exists, run it or delete the clause and restate as untested |
| "This requires investigation" | **Open-item sweep.** Go and investigate it now — control balance by dimension, then detail by dimension. Only "tried and hit a named wall" may survive to the shipped pack |
| "The pinned items explain the difference" | Sum them. If they do not equal the difference, say the decomposition does not close and quantify what is unattributed |

### Tier 3 — Adversarial independent review

An independent pass is **expected on every pack**, not reserved for unusual ones.

- **Give the reviewer the artifact and the source data — never your own summary of them.** A reviewer briefed on your conclusions will audit your conclusions, confirm what you already believe, and miss what you missed. This has been observed: a reviewer given the conclusions confirmed all of them and caught none of three critical errors.
- **Instruct the reviewer to attack, not to verify.** The brief is "find what is wrong with this pack and what is missing from it," never "check this pack."
- Ask the reviewer to look for what is *absent* — missing transactions, missing accounts, missing periods, missing systems never queried — not only for errors in what is present.
- **Use more than one reviewer, or more than one pass, with different lenses** — completeness, correctness, and "would a reader be misled by this." Where reviewers disagree, the finding stays open.
- **Treat any reviewer finding you cannot immediately disprove as open, not dismissed.** The burden is on the pack to survive, not on the reviewer to prove the fault.

### Audit outcome

Record on the Audit_Log tab: checks run, pass/fail, findings raised, corrections applied, and anything that could not be verified and why. Record Tier 2 reclassifications explicitly — the value of the audit is visible in what it *changed*, and a Tier 2 that changes nothing is usually a Tier 2 that was run in a confirming frame. If an assertion cannot be tested because later-period data does not exist, say so explicitly in the pack rather than asserting the conclusion.

## Quality gates

Before finalizing, perform these checks:

- **Live-source discovery sweep completed and recorded on Source_Sweep.**
- **AR subledger queried. AP subledger queried.** Both, every run. Any failure recorded as a High exception with the attempts named.
- All supplied files are listed in Input_Log.
- Account population verified against the live system, numeric and alphanumeric ranges and by category.
- Every real-world bank and card account has a mapped ledger account, or a Critical exception.
- Bank transactions have source traceability.
- Inflows and outflows are not sign-reversed.
- Reconciliation starts from the book opening balance, not the bank opening balance.
- GL pulled with no journal-type filter.
- Entity-level reconciliation is complete.
- Consolidated reconciliation does not hide offsetting entity issues.
- Bank-to-ERP differences are separately identified.
- Every reconciling item is bucketed as proven timing, unproven timing, or unrecorded.
- No proven-timing claim rests on a recurring-amount match.
- Test windows do not extend past the last populated ledger period.
- Carryforward balances are itemized and aged.
- Duplicate candidates are flagged.
- AR/AP conflicts with observed cash activity are flagged; disputed items are carried separately and excluded from liquidity figures, with the exclusion stated.
- Exception severities conform mechanically to the stated materiality rule.
- Accepted standing positions are carried forward, not re-raised as new findings.
- Commentary is supported by source data, and separates operating from funding inflows.
- Dashboard_Data is based on reconciled outputs, not raw unvalidated files.
- **The adversarial pre-ship audit pass has been run and its results recorded on Audit_Log.**

## Boundaries

Do not create or submit payment files.
Do not send emails.
Do not move money.
Do not post journal entries.
Do not change source files unless explicitly asked.
Do not hide material differences in consolidated totals.
Do not produce final CFO commentary before validating the reconciliation.
Do not treat the dashboard as the source of truth.
Do not describe an item as a timing difference without evidence from a later period, established by identity.
Do not declare data unavailable without exhausting the line-level object, the control account, and a second object family.
Do not build a pack before the live-source discovery sweep, including AR and AP, is complete.
Do not state a cause you have not queried, in any framing, however hedged.
Do not ship an item flagged as "requires investigation" without having investigated it.
Do not present a partial attribution as if it explained the whole difference.
Do not ship without completing the adversarial pre-ship audit pass.
