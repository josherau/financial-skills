---
name: monthly-financial-review
description: >
  Run a guided Monthly Financial Review in Claude Web using the active Claude Project
  as company context and two month-end finance workbooks as evidence. Use this skill
  when the user asks for an MFR, monthly financial review, CFO monthly review,
  actuals review, variance review, performance review, or wants to turn finance
  actuals and operating drivers into a CFO-ready HTML dashboard deck. The skill
  guides 3 to 5 compact visual review cycles, asks data-grounded multiple-choice
  and free-text questions, challenges the user instead of inventing causes, and
  produces a repeatable standalone HTML MFR deck.
---

# Monthly Financial Review Skill

<when_to_use>
Use this skill when the user wants to run a Monthly Financial Review from finance files, actuals, budget, forecast, operating drivers, KPIs, or close outputs. Use it for CFO, FP&A, board, executive, or management review workflows.

Do not use this skill for generic dashboard design, ad-hoc accounting research, document summarization, or long-form finance Q&A that does not involve producing a guided MFR and final deck.
</when_to_use>

## Core separation of responsibility

This skill contains the **process**.

The Claude Project contains the **company context**.

Use the active Project instructions as the source for company facts, business model, management priorities, materiality thresholds, terminology, business units, reporting calendar, audience, and visual style. Do not hardcode company-specific facts in this skill.

If Project context is missing or thin, proceed with the files and clearly state the limitation. Do not ask for a separate memory file. Do not require Notion, Claude Cowork, MCP, local folders, or a custom database.

## Purpose

Turn two realistic month-end finance workbooks into a guided CFO Monthly Financial Review.

The output is not only a report. The output is a structured conversation that improves the final narrative:

1. Validate the files.
2. Identify the material performance signals.
3. Show compact visual evidence.
4. Ask management judgment questions.
5. Capture user context from the answers.
6. Build a repeatable, management-ready HTML MFR deck.

## Required input

Expect two workbooks, although filenames may vary.

### 1. Financial workbook

Normally includes some combination of:

- Monthly P&L actuals.
- Actual vs budget.
- Actual vs forecast.
- Prior month, prior year, or trailing trend.
- Cash summary.
- Working capital: AR, AP, inventory, deferred revenue, accruals.
- Opex by department or function.
- Headcount, payroll, or personnel cost.
- Balance sheet or cash flow details if available.

### 2. Operating drivers workbook

Normally includes some combination of:

- Revenue by product, customer segment, region, channel, store, business unit, or product line.
- Volume, units, usage, transactions, customers, bookings, pipeline, or retention.
- Pricing, AOV, ARPU, ARR, NRR, discounting, or mix.
- Capacity, utilization, throughput, service levels, production, compute, labor hours, or delivery metrics.
- Marketing, sales, demand generation, conversion, CAC, or funnel metrics.
- Inventory, fulfillment, support, implementation, service operations, or other business drivers.

The files should look like normal finance files delivered after month-end close. Do not require LLM-specific README tabs, schema tabs, or prompt helper tabs. Infer structure from sheet names, headers, row labels, values, and formulas.

## Hard rules

1. **Do not generate the final MFR deck immediately.**
   The core value of this skill is the guided review. First run 3 to 5 review cycles.

2. **Each review cycle must include visible evidence before any question.**
   This is a non-negotiable rule. Every review cycle must render 2 to 3 metric cards and at least one compact chart or one compact table before the question tool is invoked. A cycle that shows only text and a question is invalid.

2b. **Each review cycle must fit on one screen.**
   Keep the evidence compact enough that the 2 to 3 cards, the one compact chart or one compact table, and the question tool can all fit in one screen view without scrolling.

3. **Always use the question tool for finite user choices.**
   Every multiple-choice question, confirmation question, cycle-selection question, or finite-choice user decision must be asked through Claude's question/picker tool, also known as `AskUserQuestion`. Numbered prose lists, A/B/C/D text blocks, or inline "please reply with A" questions are forbidden. A short preamble is allowed only if it is followed immediately by the question tool.

4. **Render visuals first, then use the question tool before continuing.**
   When the state machine says to ask a question, first render the required visual evidence block in chat. Only after the visual evidence block is visible may you invoke the question tool and stop. Do not continue analysis, do not answer your own question, and do not generate the next cycle or final deck until the user has answered the tool.

5. **Free-text context must also be collected through the question tool.**
   Use the tool's free-text escape hatch, custom answer field, or "Something else" capability for context. Do not print a separate prose free-text question below the picker. If the UI cannot collect free text in the same question, ask a second `AskUserQuestion` with one option such as "Add context" and rely on the free-text field.

6. **Show visible finance evidence, not hidden reasoning.**
   Do not reveal chain-of-thought or internal deliberation. Show only the evidence artifacts needed to support the question: cards, tables, bridges, trends, sparklines, or bullet-style bars. Every cycle must visibly contain 2 to 3 metric cards and at least one compact chart or one compact table. If that minimum evidence block is missing, do not ask the question yet.

7. **Questions must be data-grounded.**
   Multiple-choice answers must be created from the actual data, the Project context, and prior answers in the conversation. Do not use generic tone questions unless a final narrative posture decision is genuinely needed.

8. **Challenge the user.**
   If the data is ambiguous, present plausible interpretations and ask the user to choose or add context. Do not make up causes. The skill should make the user a better CFO, not replace the user's judgment.

9. **Use the smallest useful evidence set.**
   If the question is about a trend break, show a trend chart. If the question is about profit conversion, show a bridge. If the question is about mix, show the relevant category, segment, channel, or product table. Do not show a broad dashboard during review cycles.

10. **Stable final deck structure.**
   Every month must produce the same overall deck structure, visual language, and CSS classes. The story changes. The deck architecture does not.

11. **No external dependencies.**
   The final deck must be a single standalone HTML file using inline CSS and inline SVG or simple CSS visuals. Do not use external libraries, CDN links, remote fonts, images, scripts, private URLs, or external assets.

12. **Use Project context for company memory.**
   Treat active Project instructions as the company setup. Do not request a separate memory file. Do not write or update persistent memory systems unless the user explicitly asks.

13. **Do not over-explain the skill.**
    The user is running the workflow, not learning how to build it. Keep chat outputs concise, visual, and CFO-ready.

14. **Avoid em dashes.**
    Use periods, commas, colons, or simple hyphens instead.

## Files to read from this package

Before running the skill, consult these resources as needed:

- `resources/mfr-analysis-playbook.md` for finance logic and variance interpretation.
- `resources/review-cycle-state-machine.md` for the review workflow.
- `resources/visual-checkpoint-rules.md` for cycle evidence design.
- `resources/question-design.md` for multiple-choice and free-text question design.
- `resources/few-inspired-dashboard-rules.md` for dashboard visual principles.
- `resources/html-deck-style-guide.md` for final deck design.
- `templates/mfr-html-deck-template.html` for the final output structure.

## State machine

This skill is a state machine. After every user answer, look up the current state and execute exactly the prescribed next action. Deviating into open-ended analysis is the failure mode this skill is designed to prevent.

| State | Next action |
|---|---|
| **S0 - Invoked** | Confirm the two workbooks are attached or available. Read the active Project context. Inspect workbook sheets, headers, row labels, and available periods. Do not ask for company context if the Project already contains it. Go to S1. |
| **S1 - Input validation** | Produce a compact validation checkpoint showing workbook coverage, period detected, key sheets found, usable comparisons, missing evidence, and whether an MFR can proceed. Do not ask a question unless a critical file is missing or unreadable. Go to S2. |
| **S2 - Plan review cycles** | Select 3 to 5 review cycles based on materiality and data coverage. Always include performance signal, revenue or value driver quality, and profit conversion. Add cash/working capital and narrative resolution only when useful. Briefly list selected cycles in one compact line. Go to S3(1). |
| **S3(i) - Review cycle i** | Build one visual checkpoint using the minimum evidence required. Then invoke `AskUserQuestion` for the user judgment. The tool question must contain the multiple-choice options and a free-text escape hatch for context. Do not print the MC options as prose. Stop and wait for the user. After the user answers, store the selection and free-text context in conversation state. If more cycles remain, go to S3(i+1). Otherwise go to S4. |
| **S4 - Narrative synthesis checkpoint** | Show a compact draft MFR storyline with 3 to 5 messages and the management agenda. If prior answers conflict or the storyline remains ambiguous, invoke `AskUserQuestion` for the final confirmation. Do not ask with prose options. Otherwise proceed to S5. |
| **S5 - Final deck** | Generate the standalone HTML dashboard deck using the repeatable MFR deck structure and the Project's company style if provided. Include a short delivery note and the HTML file or full HTML artifact. Do not restart analysis unless the user requests changes. |
| **Any state - User changes scope** | Honor the change. If the change affects earlier answers, update the cycle plan or final narrative and explain the impact in one sentence. |

## Review cycle selection logic

Minimum: 3 cycles. Maximum: 5 cycles.

Always include:

1. **Performance Signal**
   - What changed this month?
   - Which variances are material?
   - Is the month better, worse, or mixed?

2. **Revenue or Value Driver Quality**
   - What drove revenue, value creation, usage, activity, output, or demand?
   - Was growth broad-based or concentrated?
   - Was the result supported by volume, price, mix, channel, product, capacity, utilization, or service activity?

3. **Profit Conversion**
   - Did revenue or activity upside convert to gross profit, contribution margin, EBITDA, operating income, cash, or another relevant profitability measure?
   - Was conversion limited by mix, discounting, COGS, Opex, headcount, delivery cost, utilization, or timing?

Add when material:

4. **Cash and Working Capital**
   - Did cash move in line with operating performance?
   - Are inventory, AR, AP, deferred revenue, collections, billing, payment timing, or capex changing the story?
   - Is the movement planned, seasonal, growth-supporting, or a warning signal?

5. **Narrative Resolution**
   - Use this when the evidence supports multiple credible narratives.
   - Use it to choose the final CFO framing before the deck.

Do not run all five cycles by default. Pick only the cycles needed for a strong MFR narrative.

## Review cycle output contract

Every review cycle must use this exact structure:

```markdown
### Review cycle {i}/{n}: {cycle name}

**Why this matters:** One sentence.

[Visual evidence block]
- 2 to 3 metric cards.
- Plus one compact chart or one compact table.
- This minimum visual block is mandatory.
- No long commentary.

**What the evidence suggests**
- Confirmed fact: ...
- Possible interpretation: ...
- What remains uncertain: ...

[Invoke `AskUserQuestion` only after the visual block is visibly rendered]
Prompt: Question {i}: Choose the strongest interpretation and add any business context.
Options: 3 to 5 data-grounded options.
Free-text/context field: Ask what the user knows from the business that would confirm, weaken, or change the interpretation.
Do not print A/B/C/D options in chat outside the tool.
```

Stop after the questions. Do not continue until the user answers.

## Multiple-choice answer rules

Each multiple-choice question must be asked with `AskUserQuestion`, not as a prose list.

Each multiple-choice question must have 3 to 5 declared options. The user-facing picker may also include an automatic free-text or "Something else" option. Use that as the context escape hatch.

Good options are:

- Mutually distinct.
- Based on the actual data shown in the checkpoint.
- Written like CFO judgment choices.
- Specific enough to influence the final MFR narrative.
- Informed by company context from the Project.
- Not just "optimistic / pessimistic / balanced."

Every question must include one option that admits uncertainty when appropriate, for example:

- "The data is inconclusive and this should remain a follow-up."
- "This looks material, but the cause cannot be confirmed from these files."

Do not include a manual "Something else" option if the question tool already provides free text. The tool's free-text capability is the escape hatch.

## Question tool hard rules

- If the user must choose from a finite set, invoke `AskUserQuestion`.
- Do not show the same finite choices as a markdown list before or after the tool.
- Do not ask the user to reply with A, B, C, D, or E.
- Do not combine multiple unrelated decisions in one tool call.
- Use one tool call per review cycle unless a separate free-text-only context question is required by the UI.
- The visual evidence must appear before the tool call, because the picker options must be grounded in the evidence shown.
- After invoking the tool, stop. Wait for the answer before advancing to the next state.
- If the question tool is unavailable, stop and tell the user the MFR Skill requires the interactive question tool for review-cycle choices.

## Recommended cycle patterns

### Performance Signal

Use when: always.

Visual evidence:

- Revenue or value metric, gross margin or contribution margin, EBITDA or operating profit, cash, working capital, and headcount cards when available.
- One compact variance table showing actual vs budget, forecast, prior month, or prior year.
- Use neutral styling for normal variation and exception highlighting only for material signals.

Question examples:

- "Which signal should anchor this month’s MFR?"
- "What is the cleanest executive read of the month?"
- "Which variance deserves management attention first?"

### Revenue or Value Driver Quality

Use when: always.

Visual evidence:

- Revenue bridge, value driver bridge, category table, channel table, product table, customer segment table, or usage trend.
- If there is a trend break, show a monthly trend chart.
- If growth is concentrated, show top contributors and the concentration percentage.

Question examples:

- "What best explains the revenue or value driver beat?"
- "How should we describe the quality of growth?"
- "Is this demand signal broad enough to update the forecast?"

### Profit Conversion

Use when: always.

Visual evidence:

- Gross margin bridge, contribution margin bridge, category margin table, or EBITDA bridge.
- Separate revenue effect, margin rate effect, Opex effect, headcount effect, and timing where possible.
- Show only the values needed to explain conversion.

Question examples:

- "Why did profit not improve more despite revenue upside?"
- "What is the strongest margin explanation?"
- "Is this a temporary mix issue or an operating model issue?"

### Cash and Working Capital

Use when: material movement in cash, inventory, AR, AP, deferred revenue, capex, billing, or collections.

Visual evidence:

- Cash bridge or working capital movement table.
- Inventory, AR, AP, deferred revenue, or collections table if available.
- If cash and EBITDA diverge, show a compact reconciliation.

Question examples:

- "How should management interpret the working capital movement?"
- "Is cash movement mostly timing, growth investment, or an early warning signal?"
- "What follow-up should be assigned before next month?"

### Narrative Resolution

Use when: prior answers or data create multiple plausible storylines.

Visual evidence:

- 3 to 5 draft messages in cards.
- One management agenda table with issue, decision, owner, and next evidence needed.

Question examples:

- "Which final MFR narrative is most defensible?"
- "What should leadership decide after reading this deck?"
- "Which message should be elevated to the executive summary?"

## Final deck structure

The final deck must always use this repeatable structure:

1. **Cover and Executive Summary**
   - Company and month.
   - Overall signal.
   - 3 key messages.
   - 3 management questions.

2. **Performance Scorecard**
   - Actual vs budget, forecast, prior month, or prior year.
   - Only material exceptions highlighted.
   - Use stable metric cards and a compact variance table.

3. **Revenue or Value Driver Quality**
   - Driver bridge or trend.
   - Segment, product, channel, region, customer, or usage table.
   - The selected interpretation from the review cycle.

4. **Margin and Profit Conversion**
   - Bridge from revenue or activity signal to profit outcome.
   - What is confirmed vs uncertain.
   - User input from the review cycle incorporated clearly.

5. **Cash and Working Capital**
   - Cash bridge or movement table when data exists.
   - Working capital interpretation.
   - Follow-ups for timing, collections, inventory, capex, or billing.

6. **Management Agenda**
   - Decisions required.
   - Follow-ups.
   - Owners if supported by company context.
   - Evidence to check next month.

7. **Appendix**
   - Source workbooks.
   - Period.
   - Assumptions.
   - Data gaps.
   - User choices from each review cycle.

If a section lacks evidence, keep the section but mark it as "not available from the uploaded files" and explain the missing evidence in one concise sentence.

## Final deck style

Use the style defined in the active Project instructions when available.

If no style is provided, use the default CFO-neutral style in `resources/html-deck-style-guide.md`:

- Off-white or light neutral background.
- Charcoal text.
- One muted accent color.
- Light gray cards and tables.
- Exception color only for material risk.
- No pie charts, donut charts, gauges, 3D, decorative icons, stock photos, or external assets.
- Print-friendly slide-like sections.

## Quality checks before final deck

Before producing the final HTML, silently verify:

- The deck uses user answers from all review cycles.
- Each major conclusion is tied to evidence from the files or user-provided context.
- Data gaps are explicitly labeled.
- Negative variances are formatted consistently.
- The deck has the same structure every month.
- The deck is a standalone HTML file.
- There are no external assets or library dependencies.
- There are no company-specific assumptions beyond Project context and uploaded files.


## Visual gating rule

A review cycle is complete only if all three conditions are met:

1. 2 to 3 metric cards are visible.
2. At least one compact chart or one compact table is visible.
3. The question tool has been invoked with multiple-choice options and free-text context capture.

If any of the three conditions are missing, the cycle is invalid. In that case, fix the cycle instead of advancing.
