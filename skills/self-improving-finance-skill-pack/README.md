# Self-Improving Finance Skill Pack

This skill pack is designed for the Born2Cycle Self-Improving Finance System demo.

It is a direct evolution of the Closed Loop Finance workflow. The goal is not to add a longer process. The goal is to add a Quality Gate and human approval step so every finance cycle can improve the next one safely.

## Structure

- `SKILL.md`: The main Self-Improving Finance wrapper skill. This is the file Claude should treat as the entry point.
- `specialist-skills/CFO_BRAIN_SKILL.md`: CFO judgment, voice, FP&A logic, escalation discipline, and approval standards for learning items.
- `specialist-skills/CFO_MEMORY_SKILL.md`: Notion-based decision memory and approved learning behavior.
- `specialist-skills/CFO_QUALITY_GATE_SKILL.md`: Evaluation layer for outputs, Learning Candidates, and CFO approval before memory promotion.
- `specialist-skills/CFO_AUDIT_SKILL.md`: Evidence, source tracking, confidence grading, and formal audit trail behavior when needed.

## Intended setup

Use this pack with:

- Claude Cowork as the finance operator.
- A shared Born2Cycle finance folder as the evidence layer.
- A Notion page named `Born2Cycle Finance Decisions Log` with a database named `Decision Log` as the structured decision and approved learning memory layer.
- A folder named `07 Quality Gates & Learning` for Quality Gate & Learning Notes.

## Demo flow

1. Set up Claude Cowork as the finance operator.
2. Set up Google Drive as the evidence layer.
3. Set up Notion as the decision and approved learning memory layer.
4. Install or reference this skill pack in the project.
5. Run the April 2026 self-improving close review prompt.
6. Claude produces the CFO close memo.
7. Claude runs the Quality Gate.
8. Claude proposes Learning Candidates.
9. The CFO approves, edits, rejects, or holds the Learning Candidates.
10. Claude writes only approved learning to Notion.
11. Next month, Claude starts with the approved learning before reviewing May.

## Core governance rule

AI proposes improvement. The Quality Gate evaluates improvement. The CFO approves improvement. Only approved learning becomes operating memory.

## Notes

The skill pack is not meant to replace accounting review, audit procedures, legal advice, or CFO judgment. It is a workflow layer for making finance work more traceable, repeatable, memory-driven, and safely self-improving.
