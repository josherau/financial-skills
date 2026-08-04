# Financial Skills

This repository stores Joshua Thompson's financial and CFO skill library as installable `.skill` packages and extracted source folders.

This repository keeps both:

- installable `.skill` bundles in `packages/`
- extracted, readable source folders in `skills/`

Use `DIRECTORY.md` as the human-facing map of what each skill does, when to use it, expected inputs, outputs, and important controls.

## Repository Layout

```text
financial-skills/
├── DIRECTORY.md
├── README.md
├── USING_SKILLS.md
├── packages/
│   └── *.skill
└── skills/
    ├── born2cycle-monthly-snapshot/
    ├── cash-flow-model-builder/
    ├── cfo-audit-trail/
    ├── cfo-board-prep/
    ├── cfo-brain/
    ├── cash-reconciliation-reporting/
    ├── cfo-cash-dashboard/
    ├── cfo-memory/
    ├── cfo-quality-gate/
    ├── forensic-finance-investigation/
    ├── monthly-financial-review/
    └── self-improving-finance-skill-pack/
```

## Included Skill Families

| Skill | Primary job |
| --- | --- |
| `born2cycle-monthly-snapshot` | Generate the governed Born2Cycle CFO monthly snapshot from Finstory data. |
| `cash-flow-model-builder` | Build a simple Week 0 13-week cash flow forecast workbook. |
| `cash-reconciliation-reporting` | Run a finance-grade bank-to-ledger cash reconciliation workflow. |
| `cfo-board-prep` | Prepare CFOs for board, investor, lender, finance committee, and audit committee meetings. |
| `cfo-brain` | CFO judgment, voice, board prep, covenants, M&A, capital allocation, and governance. |
| `cfo-cash-dashboard` | Turn a completed reconciliation pack into a CFO-ready cash dashboard. |
| `cfo-memory` | Decision memory, evidence memory, pattern memory, and approved learning memory. |
| `cfo-audit-trail` | Defensible audit trail entries for material CFO outputs. |
| `cfo-quality-gate` | Evaluation layer for outputs and proposed learning candidates. |
| `forensic-finance-investigation` | Investigate finance packs where the reported story and cash reality do not line up. |
| `monthly-financial-review` | Run a guided monthly financial review and build an HTML dashboard deck. |
| `self-improving-finance` | Coordinate recursive finance memory, quality gates, audit, and approved learning. Source folder: `skills/self-improving-finance-skill-pack/`. |

The `skills/self-improving-finance-skill-pack/` folder also includes specialist CFO stack skills:

- `CFO_BRAIN_SKILL.md` - CFO judgment, voice, board prep, covenants, M&A, capital allocation, and governance.
- `CFO_MEMORY_SKILL.md` - decision memory, evidence memory, pattern memory, and approved learning memory.
- `CFO_AUDIT_SKILL.md` - defensible audit trail entries for material CFO outputs.
- `CFO_QUALITY_GATE_SKILL.md` - evaluation layer for outputs and proposed learning candidates.

## How To Use This Repo

1. Read `DIRECTORY.md` to choose the right skill.
2. Use the extracted folder under `skills/<skill-name>/` when editing or reviewing instructions.
3. Use the packaged file under `packages/<skill-name>.skill` when installing or moving a bundled skill.
4. Preserve bundled assets and templates exactly unless you are intentionally updating the skill version.

## Update Rule

When changing a skill, update the extracted source first, rebuild the `.skill` package if needed, and update `DIRECTORY.md` when the skill's use case, inputs, outputs, or critical controls change.

Initial source import: local files under `/Users/jthompson/Projects/AI CFO/` plus `CFO_Board_Prep_SKILL.md` from `/Users/jthompson/Downloads/` on 2026-08-04. See `SOURCE_INVENTORY.md`.
