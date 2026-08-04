# Review Cycle State Machine

## Principle

The review cycles are the product. Do not collapse them into a single analysis dump.

Each cycle should make the user smarter about one financial question. The visual evidence should be exactly the evidence required to answer that question.

Every cycle must first render a mandatory visual checkpoint, then end with an `AskUserQuestion` tool call. Markdown questions are not enough. The tool call is the state transition gate.

## Cycle planning

After validation, select 3 to 5 cycles.

Always choose based on:

1. Materiality.
2. Data availability.
3. Narrative importance.
4. Need for human judgment.

Do not choose cycles just because a file contains a sheet. A sheet is not a question.

## Required cycles

### 1. Performance Signal

Purpose: Find the main signal of the month.

Evidence pattern:

- 2 to 3 cards for the most important KPIs.
- One compact variance table or one compact trend chart.
- 3 evidence bullets.
- The visual block must be visible before the question tool appears.

Question tool pattern:

Invoke `AskUserQuestion` with a prompt like: "Which signal should anchor this month’s MFR?" and 3 to 5 data-grounded options.

### 2. Revenue or Value Driver Quality

Purpose: Explain whether growth or activity quality is strong, concentrated, low-quality, timing-driven, or unclear.

Evidence pattern:

- 2 to 3 driver cards.
- One bridge, trend, or segment table.
- 3 evidence bullets.
- The visual block must be visible before the question tool appears.

Question tool pattern:

Invoke `AskUserQuestion` with a prompt like: "How should we describe the quality of this growth or activity signal?" and 3 to 5 data-grounded options.

### 3. Profit Conversion

Purpose: Explain why revenue or activity did or did not convert into profit.

Evidence pattern:

- 2 to 3 profit cards.
- One bridge or margin table.
- 3 evidence bullets.
- The visual block must be visible before the question tool appears.

Question tool pattern:

Invoke `AskUserQuestion` with a prompt like: "What is the strongest explanation for profit conversion?" and 3 to 5 data-grounded options.

## Optional cycles

### 4. Cash and Working Capital

Use only when cash, AR, AP, inventory, deferred revenue, capex, collections, billing, or working capital materially changes the narrative.

### 5. Narrative Resolution

Use only when the first cycles leave two or more defensible executive narratives.

## How to handle user answers

After each answer:

- Treat the multiple-choice answer as management judgment.
- Treat the free-text answer as management context.
- Carry both into later cycles.
- Mark management context as unverified when not directly supported by the files.
- If the user's context contradicts the files, state the tension and keep both visible.

## Autopilot prevention

These are bugs:

- Asking a finite-choice question in prose instead of invoking `AskUserQuestion`.
- Invoking `AskUserQuestion` before the cards and chart-or-table are visibly rendered.
- Running a cycle with cards only and no chart or table.
- Running a cycle with a chart or table only and no cards.
- Printing A/B/C/D options in chat and asking the user to reply.
- Asking a free-text context question in prose when the question tool's free-text escape hatch should be used.
- Continuing to the next cycle before the user answers the current tool question.
- Building the final deck before the review cycles finish.
- Asking broad questions before showing evidence.
- Showing a full dashboard instead of a focused checkpoint.
- Using generic answer options not based on the current data.
- Treating ambiguous data as a known cause.
- Skipping the free-text question.
- Asking more than one multiple-choice question per cycle.
- Running more than five cycles.
- Changing the final deck structure based on the month.


## Mandatory cycle validity check

Before invoking `AskUserQuestion`, confirm mentally that the cycle contains:

1. 2 to 3 metric cards.
2. One compact chart or one compact table.
3. Three short evidence bullets.

If any item is missing, do not ask the question yet. First fix the visual checkpoint.
