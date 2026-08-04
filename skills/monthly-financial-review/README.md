# Monthly Financial Review Skill

This is a Claude Skill package for running a guided CFO Monthly Financial Review in Claude Web.

## Use case

Upload this Skill to Claude. Use it inside a Claude Project that contains company context. Then attach two normal month-end workbooks:

1. Financial workbook
2. Operating drivers workbook

Run:

```text
Run the Monthly Financial Review Skill using the two attached finance files.
```

The Skill will guide 3 to 5 review cycles. Each cycle shows a compact visual evidence checkpoint, asks one multiple-choice question, and asks one free-text context question. After the review cycles, it creates a standalone HTML MFR deck.

## What belongs in the Project

The Project should contain company context, such as:

- Company description.
- Business model.
- Products, segments, regions, channels, entities, or departments.
- Management priorities.
- Reporting audience.
- Materiality thresholds.
- Known seasonality.
- Preferred terminology.
- Visual style preferences.

## What belongs in the Skill

The Skill contains the MFR process:

- Input validation.
- Review cycle selection.
- Visual evidence checkpoints.
- Multiple-choice judgment questions.
- Free-text context capture.
- Narrative synthesis.
- Repeatable HTML deck generation.

## What this Skill does not do

- It does not require Claude Cowork.
- It does not require an MCP server.
- It does not build a Notion memory system.
- It does not require a separate memory file.
- It does not contain company-specific facts.
- It does not teach the reader how to build a Skill.

## Package contents

- `SKILL.md` - Skill entrypoint and workflow.
- `resources/mfr-analysis-playbook.md` - Finance analysis logic.
- `resources/review-cycle-state-machine.md` - State machine for guided review cycles.
- `resources/visual-checkpoint-rules.md` - Review-cycle visual rules.
- `resources/question-design.md` - Multiple-choice and free-text question patterns.
- `resources/few-inspired-dashboard-rules.md` - Dashboard design principles.
- `resources/html-deck-style-guide.md` - Final deck visual structure.
- `templates/mfr-html-deck-template.html` - Repeatable HTML deck template.
- `examples/run_prompt.txt` - Suggested run prompt.
- `examples/project-context-template.md` - Optional template for users creating their own Project instructions.


## Interactive question requirement

During every review cycle, the Skill must use Claude's question/picker tool (`AskUserQuestion`) for finite-choice decisions. The Skill should not ask users to pick from markdown A/B/C/D lists.
