# Question Design

## Purpose

The questions are the workflow.

The Skill should not pretend to know the business cause when the files only show financial symptoms. The multiple-choice question should force the user to choose the most defensible interpretation, and the free-text question should capture business context.

## Non-negotiable tool rule

Every finite-choice question must be asked through Claude's question/picker tool, `AskUserQuestion`. A markdown list of options is not an interactive question and is not allowed. The visual checkpoint may be rendered in chat, but the choice itself must be a tool call.

## Question structure

Each review cycle asks one tool-based question using `AskUserQuestion`.

The tool question must include:

1. A multiple-choice judgment prompt.
2. 3 to 5 declared options.
3. A free-text escape hatch for business context, using the tool's built-in free-text, custom answer, or automatic "Something else" behavior.

Do not print the options as markdown. Do not ask the user to answer with A/B/C/D. The user must be able to click the options in the interface.

Recommended tool shape:

```text
AskUserQuestion
Prompt: Question {i}: Choose the strongest interpretation. Add context if the files do not tell the whole story.
Options:
- [data-grounded option 1]
- [data-grounded option 2]
- [data-grounded option 3]
- [uncertainty/follow-up option when appropriate]
Free-text/context hint: What business context would confirm, weaken, or change this interpretation?
```

If the UI does not support a free-text field in the same picker, ask a second `AskUserQuestion` immediately after the selection with a single option such as "Add context" and rely on the tool's free-text field. Do not use prose as the fallback.

## What makes a good multiple-choice option

A good option:

- Reflects a plausible CFO interpretation.
- Is based on data shown in the checkpoint.
- Uses Project context when relevant.
- Creates a meaningful difference in the final narrative.
- Avoids generic tone language.
- Is specific enough that choosing it changes the MFR deck.

Bad options:

- "Everything is fine."
- "Needs more analysis."
- "Positive / neutral / negative."
- "Focus on growth / focus on margin" when the data suggests a more specific choice.
- Any option that uses numbers not shown in the evidence block.

## Number of options

Use 3 to 5 options. Never exceed 5 declared options in the question tool. The automatic free-text or "Something else" escape hatch does not count as one of the declared options.

Default pattern:

- A = most direct explanation supported by the data.
- B = credible alternate explanation from company context.
- C = risk-oriented interpretation.
- D = uncertainty or follow-up option.
- E = only when there is a true fifth interpretation.

## Free-text context capture

The free-text context field in `AskUserQuestion` should ask for business context, not a rewrite.

Good:

- "What do you know from the business that would confirm or weaken this interpretation?"
- "Was there a pricing change, customer event, supplier issue, operational bottleneck, timing item, or one-time adjustment not visible in the files?"
- "Should this be treated as a one-time timing item or a recurring issue?"

Bad:

- "Any comments?"
- "Anything else?"
- "Do you want this to be more positive?"

## How to use answers

After the user answers:

- Treat multiple-choice selection as a user judgment.
- Treat free-text as additional context.
- Do not let free-text override hard data unless the user explicitly explains why.
- Carry answers forward into later questions.
- Use the answers in the final deck appendix as "management input from review cycle."

## If the user gives a weak or unclear answer

Do not scold. Use it.

Example:

- User says: "Probably B, but not sure."
- Response should treat B as the working hypothesis and mark the related conclusion as "likely, pending follow-up."

If ambiguity materially affects the final deck, use the Narrative Resolution cycle.

## Smart question examples

### Performance Signal

Question:
"Which signal should anchor this month’s MFR?"

Options:

A. Revenue outperformance is real, but profitability did not convert as expected.
B. The month is mainly a margin story because mix, pricing, or delivery costs diluted the revenue beat.
C. Working capital movement is the key risk because cash absorbed the operating upside.
D. The data is mixed and should be framed as a balanced review with explicit follow-ups.

### Revenue or Value Driver Quality

Question:
"How should we describe the growth signal?"

Options:

A. Broad-based demand improvement across the main drivers.
B. Concentrated growth in one product, segment, region, or channel that may not generalize.
C. Promotion, timing, or mix-driven growth that needs margin validation.
D. The beat is valid, but the files do not prove whether it is repeatable.

### Profit Conversion

Question:
"What is the strongest explanation for profit conversion?"

Options:

A. Revenue upside was offset by lower-margin mix.
B. Pricing, discounting, input cost, or delivery cost pressure reduced margin.
C. Opex, headcount, or investment pace absorbed the upside.
D. The data is inconclusive and this should remain a follow-up.

### Cash and Working Capital

Question:
"How should management interpret the cash movement?"

Options:

A. Mostly timing, with no immediate change to operating read.
B. A growth-supporting working capital investment.
C. A warning signal that needs owner-level follow-up before next month.
D. Inconclusive because the files do not show enough billing, collections, or payment detail.


## Forbidden question patterns

- Writing: `Question 1A` followed by A/B/C/D options in prose.
- Writing: `Please reply A, B, C, or D`.
- Showing a numbered or bulleted list of options and waiting for a chat reply.
- Asking a free-text question in prose after a picker when the same context should be captured in the question tool.
- Asking the next review-cycle question before the user has answered the current `AskUserQuestion`.
- Generating the final deck without all required picker answers.
