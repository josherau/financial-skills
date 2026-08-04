# Source Inventory

This file records what was imported from the local AI CFO source folder and what was intentionally left out.

## Imported Skill Sources

| Source | Repo destination |
| --- | --- |
| `/Users/jthompson/Projects/AI CFO/born2cycle-monthly-snapshot.skill` | `packages/koen-advisors-sample-monthly-snapshot.skill`; `skills/koen-advisors-sample-monthly-snapshot/` |
| `/Users/jthompson/Projects/AI CFO/cash-flow-model-builder.skill` | `packages/cash-flow-model-builder.skill`; `skills/cash-flow-model-builder/` |
| `/Users/jthompson/Projects/AI CFO/cash-reconciliation-reporting.skill` | `packages/cash-reconciliation-reporting.skill`; `skills/cash-reconciliation-reporting/` |
| `/Users/jthompson/Projects/AI CFO/cfo-cash-dashboard.skill` | `packages/cfo-cash-dashboard.skill`; `skills/cfo-cash-dashboard/` |
| `/Users/jthompson/Projects/AI CFO/forensic-finance-investigation.skill` | `packages/forensic-finance-investigation.skill`; `skills/forensic-finance-investigation/` |
| `/Users/jthompson/Projects/AI CFO/monthly-financial-review.skill` | `packages/monthly-financial-review.skill`; `skills/monthly-financial-review/` |
| `/Users/jthompson/Projects/AI CFO/self-improving-finance-skill-pack.zip` | `packages/self-improving-finance-skill-pack.zip`; `skills/self-improving-finance-skill-pack/` |
| `/Users/jthompson/Downloads/CFO_Board_Prep_SKILL.md` | `skills/cfo-board-prep/SKILL.md` |
| `self-improving-finance-skill-pack/specialist-skills/CFO_BRAIN_SKILL.md` | `skills/cfo-brain/SKILL.md`; original also preserved in the pack folder |
| `self-improving-finance-skill-pack/specialist-skills/CFO_MEMORY_SKILL.md` | `skills/cfo-memory/SKILL.md`; original also preserved in the pack folder |
| `self-improving-finance-skill-pack/specialist-skills/CFO_AUDIT_SKILL.md` | `skills/cfo-audit-trail/SKILL.md`; original also preserved in the pack folder |
| `self-improving-finance-skill-pack/specialist-skills/CFO_QUALITY_GATE_SKILL.md` | `skills/cfo-quality-gate/SKILL.md`; original also preserved in the pack folder |

## Imported Sample Packs

These packs are sample data/workpaper assets rather than installable skills. Repo-facing artifact names use Koen Advisors sample branding; Born2Cycle remains the fictional demo company inside the files.

| Source | Repo destination |
| --- | --- |
| `/Users/jthompson/Projects/AI CFO/data_pack.zip` and `/Users/jthompson/Projects/AI CFO/data_pack/` | `sample-packs/koen-advisors-finance-data-pack/`; `sample-packs/packages/koen-advisors-finance-data-pack.zip` |
| `/Users/jthompson/Projects/AI CFO/Born2Cycle_Self_Improving_Finance_GDrive_Starter.zip` and `/Users/jthompson/Projects/AI CFO/Born2Cycle_Self_Improving_Finance_GDrive_Starter/` | `sample-packs/koen-advisors-self-improving-finance-gdrive-starter/`; `sample-packs/packages/koen-advisors-self-improving-finance-gdrive-starter.zip` |

## Excluded Local Files

These nearby files were not imported because they are rendered output or system metadata rather than skill source or sample-pack content:

| Source | Reason excluded |
| --- | --- |
| `/Users/jthompson/Projects/AI CFO/view.html` | Local rendered/output view, not skill source. |
| `/Users/jthompson/Projects/AI CFO/.DS_Store` | macOS metadata. |
