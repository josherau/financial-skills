# Version Notes

## 2026.05.28 Self-Improving Finance update

This package adapts the original Closed Loop Finance skill pack for recursive self-improvement.

Key changes:

1. Renamed the wrapper skill to `self-improving-finance`.
2. Added Quality Gate behavior to evaluate outputs before they become final.
3. Added Learning Candidates as draft improvements that require CFO approval.
4. Added Approved Learning as the only learning that may be promoted to memory.
5. Added a dedicated `CFO_QUALITY_GATE_SKILL.md` specialist skill.
6. Updated CFO Memory so Notion can store approved learning without treating every AI suggestion as memory.
7. Updated CFO Brain with CFO-style governance rules for approving, editing, rejecting, or holding learning items.
8. Updated Audit behavior so audit trail and Quality Gate are clearly separated.
9. Replaced the generic Audit Note emphasis with the `Quality Gate & Learning Note` for the newsletter workflow.
10. Preserved the original Google Drive + Notion + Claude Cowork architecture to avoid making the workflow longer.
