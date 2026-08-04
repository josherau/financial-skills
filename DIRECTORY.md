# Financial Skills Directory

This directory is the map for choosing and using the finance skills in this repo.

## Quick Selector

| Need | Use this skill | Why |
| --- | --- | --- |
| Governed monthly CFO snapshot for Born2Cycle | `born2cycle-monthly-snapshot` | Fixed-design Finstory-powered HTML snapshot with KPIs, trends, bridge, liquidity, working capital, CCC, entity mix, and cost-of-sales variance. |
| First-pass 13-week cash forecast | `cash-flow-model-builder` | Builds a simple Week 0 Excel model from messy finance exports without overbuilding a full audit trail or scenario engine. |
| Controlled bank-to-ERP cash reconciliation | `cash-reconciliation-reporting` | Normalizes cash data, reconciles by entity/account/consolidated, forces AR/AP/source-system sweep, investigates anomalies, and produces a CFO-ready reconciliation pack. |
| Board, investor, lender, or audit committee prep | `cfo-board-prep` | Predicts director questions, builds evidence-backed answers, finds missing support, drafts opening narratives, reviews board packs, and creates pre-board risk registers. |
| Executive dashboard from a completed cash rec | `cfo-cash-dashboard` | Uses the reconciliation pack as source of truth and turns reconciled data into cash position, movement, exception, driver, and AR/AP visuals. |
| CFO forensic review of suspicious finance data | `forensic-finance-investigation` | Cross-checks revenue, EBITDA, cash, working capital, forecast, and board narrative for root causes and evidence-backed findings. |
| Guided monthly financial review | `monthly-financial-review` | Runs 3-5 visual review cycles before producing a CFO-ready HTML MFR deck from month-end finance and operating-driver workbooks. |
| Finance operating-system memory and improvement loop | `self-improving-finance` | Coordinates CFO judgment, decision memory, audit, quality gates, and approved learning so finance workflows improve over time. Source folder: `self-improving-finance-skill-pack`. |
| CFO judgment and voice layer | `cfo-brain` | CFO judgment, frameworks, board prep, covenants, M&A, capital allocation, governance, and executive pushback. |
| CFO decision and learning memory | `cfo-memory` | Evidence memory, decision memory, pattern memory, and approved learning memory. |
| CFO audit trail | `cfo-audit-trail` | Defensible output logs, source trails, confidence grades, and review rationale. |
| CFO quality gate | `cfo-quality-gate` | Evaluation layer for finance outputs and proposed learning before CFO approval. |

## Skill Details

### `born2cycle-monthly-snapshot`

**Path:** `skills/born2cycle-monthly-snapshot/`

**Packaged file:** `packages/born2cycle-monthly-snapshot.skill`

**Use when:** The user asks for the Born2Cycle CFO monthly snapshot, monthly finance snapshot, month-end report, or a snapshot for a named month/year.

**Primary inputs:**

- Finstory data-analysis connector access for Born2Cycle
- Reporting period from the user or Finstory `defaultPov`
- Required year and period members
- Required KPI library members

**Primary output:** A single-page HTML report named like `Born2Cycle_Monthly_Snapshot_May_2026.html`.

**Supporting files:**

- `assets/template.html` - governed fixed-design report template

**Critical controls:**

- Do not redesign the dashboard.
- Use the exact query playbook in `SKILL.md`.
- Stop rather than publish if required monthly data, budget data, trend history, or balance-sheet balances are missing.
- Use YTD view for closing balance-sheet balances.

### `cash-flow-model-builder`

**Path:** `skills/cash-flow-model-builder/`

**Packaged file:** `packages/cash-flow-model-builder.skill`

**Use when:** The user needs a simple first-version 13-week cash flow forecast from finance exports.

**Primary inputs:**

- Finance exports with cash-related data
- AR/AP or expected receipt/payment schedules where available
- Opening cash and weekly period information

**Primary output:** `week0_13_week_cash_flow_forecast.xlsx`

**Supporting files:** None bundled.

**Critical controls:**

- Keep the model simple and demo-friendly.
- Do not build a full row-level audit trail.
- Do not expand scope into multi-entity, multi-currency, covenant, or advanced scenario modeling unless a separate skill is used.
- Include self-checks and exceptions before finalizing.

### `cash-reconciliation-reporting`

**Path:** `skills/cash-reconciliation-reporting/`

**Packaged file:** `packages/cash-reconciliation-reporting.skill`

**Use when:** The user needs a finance-grade cash reconciliation pack from live systems, bank data, ledger exports, AR/AP, card/expense platforms, and supporting files.

**Primary inputs:**

- Live ERP/general ledger access where available
- AR and AP subledger access
- Bank statements or cash transaction exports
- Card, expense, payment processor, payroll, and treasury sources when connected
- Prior reconciliation packs or workpapers when available

**Primary output:** A controlled cash reconciliation workbook with tabs such as `Source_Sweep`, `Input_Log`, `Bank_Normalized`, `ERP_Cash_GL`, `Bank_vs_ERP_Reconciliation`, `Open_Items_Aging`, `Exception_Log`, `Dashboard_Data`, `Executive_Summary`, and `Audit_Log`.

**Supporting files:** None bundled.

**Critical controls:**

- Run the live-source discovery sweep before opening files.
- Query AR and AP every run; failures are high-severity exceptions.
- Start from book opening balance, not bank opening balance.
- Pull GL with no journal-type filter.
- Prove timing differences by identity in later periods; otherwise bucket as unproven or unrecorded.
- Research every cause and investigate every anomaly in the same pass.
- Run the adversarial pre-ship audit before delivery.

### `cfo-board-prep`

**Path:** `skills/cfo-board-prep/`

**Packaged file:** None bundled as `.skill`; source is preserved as `SKILL.md`.

**Use when:** The user is preparing for a board meeting, investor update, audit committee meeting, finance committee meeting, lender update, or leadership review.

**Primary inputs:**

- Current and prior board decks
- CFO or management letters
- Financial statements and monthly reporting packs
- Board meeting transcripts, minutes, investor emails, or internal evidence files
- Known board member names, roles, personalities, and concerns when available

**Primary output:** Board-prep package with likely questions, evidence-backed answers, missing support, opening narrative, board-pack review, and pre-board risk register.

**Supporting files:** None bundled.

**Critical controls:**

- Use only provided files when the user restricts evidence.
- Do not invent numbers, board concerns, quotes, or evidence.
- Separate strong answers from weak answers.
- Identify where trust could break before the meeting.

### `cfo-cash-dashboard`

**Path:** `skills/cfo-cash-dashboard/`

**Packaged file:** `packages/cfo-cash-dashboard.skill`

**Use when:** A completed cash reconciliation pack already exists and the user wants a CFO-ready dashboard and executive narrative.

**Primary inputs:**

- Completed reconciliation pack
- Dashboard-ready data, exception log, cash driver commentary, AR/AP summaries, and executive summary where available

**Primary output:** A CFO dashboard or report showing cash position, cash movement, bank-vs-ERP differences, exceptions, drivers, and AR/AP context.

**Supporting files:** None bundled.

**Critical controls:**

- Treat the reconciliation pack as the controlled source of truth.
- Do not redo the reconciliation unless data is missing, inconsistent, or the user explicitly asks.
- Flag conflicts between dashboard data and reconciliation tables.
- Ask concise multiple-choice clarification questions only when material.

### `forensic-finance-investigation`

**Path:** `skills/forensic-finance-investigation/`

**Packaged file:** `packages/forensic-finance-investigation.skill`

**Use when:** The finance story looks acceptable on the surface but cash, working capital, forecast accuracy, close quality, or board narrative risk does not make sense.

**Primary inputs:**

- Monthly finance packs
- P&L, cash, AR, AP, inventory, forecast, sales, customer, vendor, refund, chargeback, processor, or board-pack files
- Management commentary or hypotheses where available

**Primary output:** CFO-ready forensic investigation memo and visual finance report with quantified root causes, evidence, confidence levels, and recommended actions.

**Supporting files:** None bundled.

**Critical controls:**

- Investigate rather than summarize.
- Treat management commentary as a hypothesis.
- Connect evidence across files.
- Prioritize material drivers.
- Separate confirmed, likely, and unresolved findings.
- Avoid accusations without evidence.

### `monthly-financial-review`

**Path:** `skills/monthly-financial-review/`

**Packaged file:** `packages/monthly-financial-review.skill`

**Use when:** The user wants an MFR, monthly financial review, CFO monthly review, actuals review, variance review, performance review, or CFO-ready HTML dashboard deck.

**Primary inputs:**

- Month-end financial workbook
- Operating drivers workbook
- Active project/company context when available
- User answers from guided review cycles

**Primary output:** A standalone HTML monthly financial review deck.

**Supporting files:**

- `README.md`
- `examples/project-context-template.md`
- `examples/run_prompt.txt`
- `resources/few-inspired-dashboard-rules.md`
- `resources/html-deck-style-guide.md`
- `resources/mfr-analysis-playbook.md`
- `resources/question-design.md`
- `resources/review-cycle-state-machine.md`
- `resources/visual-checkpoint-rules.md`
- `templates/mfr-html-deck-template.html`

**Critical controls:**

- Do not generate the final MFR deck immediately.
- Run 3-5 review cycles first.
- Challenge the user with data-grounded questions instead of inventing causes.
- Use project context for company facts; do not hardcode company-specific facts into the skill.
- Preserve the HTML deck process and visual checkpoint rules.

### `self-improving-finance`

**Path:** `skills/self-improving-finance-skill-pack/`

**Packaged file:** Not included as a `.skill` bundle in `packages/`; source folder is preserved directly.

**Use when:** The finance workflow itself needs memory, governance, quality gates, audit trails, and approved-learning loops across close, forecast, board, and management cycles.

**Primary inputs:**

- Finance evidence folder
- Structured decision memory such as Notion Decision Log
- Current finance output or workflow being evaluated
- CFO approval for any learning that becomes operating memory

**Primary output:** A governed improvement loop that captures decisions, tests outcomes, proposes learning, routes learning through a quality gate, and preserves approved memory.

**Supporting files:**

- `README.md`
- `VERSION_NOTES.md`
- `specialist-skills/CFO_AUDIT_SKILL.md`
- `specialist-skills/CFO_BRAIN_SKILL.md`
- `specialist-skills/CFO_MEMORY_SKILL.md`
- `specialist-skills/CFO_QUALITY_GATE_SKILL.md`

**Critical controls:**

- Financial evidence stays in files; Notion stores decisions and approved learning.
- AI proposes improvement; the quality gate evaluates it; the CFO approves it.
- Learning candidates are not active memory until approval.
- Use the specialist skills for CFO judgment, memory, audit, and quality review.

### `cfo-brain`

**Path:** `skills/cfo-brain/`

**Packaged file:** None bundled as `.skill`; canonical standalone source is preserved as `SKILL.md`. Original pack copy remains at `skills/self-improving-finance-skill-pack/specialist-skills/CFO_BRAIN_SKILL.md`.

**Use when:** The finance work needs CFO judgment, board-safe language, FP&A standards, capital allocation thinking, covenant analysis, M&A reasoning, audit committee preparation, AI governance, or executive pushback.

**Primary inputs:**

- User question or draft finance output
- Source files or evidence layer when available
- Current strategic or governance decision

**Primary output:** CFO-level advice, framing, questions, confidence-tagged recommendations, or governance-aware response.

**Supporting files:** None bundled beyond this specialist skill file.

**Critical controls:**

- Push back when the user is about to make a finance mistake.
- Use source files as source of truth when provided.
- Search for fresh data when the question requires current external facts.
- Escalate material events such as covenant breach, going concern, material weakness, or fraud.

### `cfo-memory`

**Path:** `skills/cfo-memory/`

**Packaged file:** None bundled as `.skill`; canonical standalone source is preserved as `SKILL.md`. Original pack copy remains at `skills/self-improving-finance-skill-pack/specialist-skills/CFO_MEMORY_SKILL.md`.

**Use when:** A finance workflow needs durable memory for decisions, outcomes, variances, stakeholder patterns, or approved learning.

**Primary inputs:**

- Finance evidence layer
- Notion Decision Log or equivalent structured decision store
- Current decision, outcome, variance, or learning candidate

**Primary output:** Structured memory entry, approved learning memory, or pattern memory update.

**Supporting files:** None bundled beyond this specialist skill file.

**Critical controls:**

- Treat files as financial source of truth.
- Treat Notion as decision and approved-learning memory, not as financial truth.
- Do not promote AI-generated learning into active memory without CFO approval.
- Say what evidence is missing when the memory entry cannot be supported.

### `cfo-audit-trail`

**Path:** `skills/cfo-audit-trail/`

**Packaged file:** None bundled as `.skill`; canonical standalone source is preserved as `SKILL.md`. Original pack copy remains at `skills/self-improving-finance-skill-pack/specialist-skills/CFO_AUDIT_SKILL.md`.

**Use when:** A material CFO output needs a defensible record of what was produced, what evidence was used, who reviewed it, and why the conclusion was reached.

**Primary inputs:**

- Final or material finance output
- Source evidence and inputs
- Reviewer identity or review result
- Confidence grades and decision rationale

**Primary output:** Audit trail entry suitable for `AUDIT.md` or the configured audit record.

**Supporting files:** None bundled beyond this specialist skill file.

**Critical controls:**

- Record contradictory or inconsistent evidence, not only support for the final conclusion.
- Keep audit trail separate from learning memory.
- Do not log casual scratch work unless the user or materiality requires it.
- Preserve source, timestamp, reviewer, and rationale.

### `cfo-quality-gate`

**Path:** `skills/cfo-quality-gate/`

**Packaged file:** None bundled as `.skill`; canonical standalone source is preserved as `SKILL.md`. Original pack copy remains at `skills/self-improving-finance-skill-pack/specialist-skills/CFO_QUALITY_GATE_SKILL.md`.

**Use when:** A finance output must be evaluated before it influences a decision, or when the system needs to identify what should improve next cycle.

**Primary inputs:**

- Finance output to evaluate
- Evidence layer
- Applicable standards or approval criteria
- Candidate learning or process change, if any

**Primary output:** Quality Gate and Learning Note with pass/review/fail findings, gaps, and proposed learning candidates.

**Supporting files:** None bundled beyond this specialist skill file.

**Critical controls:**

- Evaluate source grounding, finance logic, completeness, risk, and learning quality.
- Do not produce the first answer; evaluate the answer.
- Learning candidates require CFO approval before becoming memory.
- Reject improvements that overfit one exception or create process burden without evidence.

## Suggested Workflow

1. Choose the skill from the Quick Selector.
2. Read the skill's `SKILL.md` in full before running it.
3. Read only the supporting files referenced by that skill.
4. Use source data as the source of truth; do not infer missing financial facts from examples.
5. Produce the required output format.
6. Run the skill's validation, quality, and audit gates before delivery.

## Packaging Notes

The `.skill` files in `packages/` are zip-format bundles. The extracted folders in `skills/` are the readable/editable source copies. If a bundle includes templates or assets, they are preserved under the corresponding skill folder.

Existing package root layouts:

| Package | Archive layout to preserve |
| --- | --- |
| `born2cycle-monthly-snapshot.skill` | root folder `born2cycle-monthly-snapshot/` |
| `cash-flow-model-builder.skill` | root folder `cash-flow-model-builder/` |
| `cash-reconciliation-reporting.skill` | root folder `cash-reconciliation-reporting/` |
| `cfo-cash-dashboard.skill` | root folder `cfo-cash-dashboard/` |
| `forensic-finance-investigation.skill` | rootless `SKILL.md` |
| `monthly-financial-review.skill` | root folder `monthly-financial-review-skill/` |
| `self-improving-finance-skill-pack.zip` | root folder `self-improving-finance-skill-pack/` |
| standalone CFO stack skills | source folders only; no `.skill` packages in this repo |
