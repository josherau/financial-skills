# CFO_AUDIT_SKILL

---

name: CFO Audit Trail

version: 2026.05.28

last_updated: 2026-05-28

description: Audit trail layer for the CFO Brain skill stack. Logs every meaningful output (board narratives, covenant memos, M&A recommendations, capital allocation decisions, AI capex justifications, material weakness disclosures, earnings call Q&A war-gaming, scenario forecasts, valuation work) with timestamps, inputs, sources, confidence grades, and decision rationale. Designed to be defensible to an audit committee, external auditor, regulator, or in litigation. Aligned to PCAOB AS 1215, AICPA AU-C 230, SOX Section 302/404, COSO 2013.

---

# PURPOSE

CFOs sign Section 302 sub-certifications. CFOs get sued. CFOs get deposed. CFOs leave companies and want a clean record of what they decided and why. CFOs become the comment-letter respondent for an AI claim made eighteen months ago.

The work product Claude helps produce should leave a defensible trail. That is what [AUDIT.md](http://AUDIT.md) is for. [AUDIT.md](http://AUDIT.md) is the formal record. [MEMORY.md](http://MEMORY.md) is the pattern-recognition layer. They do not duplicate each other.

This skill is anchored in:

- **PCAOB AS 1215** "Audit Documentation," paragraph .06: documentation must clearly demonstrate that the work was in fact performed, who performed the work, the person or persons who reviewed the work, and the date of such review. The "experienced auditor" reperformance test (paragraph .06A): documentation must enable an experienced auditor with no previous connection to understand nature, timing, extent, results, and conclusions, and to identify who performed and reviewed each step. Paragraph .08: documentation must include information inconsistent with or contradicting final conclusions.
- **AICPA AU-C Section 230** "Audit Documentation," paragraph .08: documentation must enable an experienced auditor with no previous connection to understand nature, timing, and extent of procedures; results and evidence; significant findings, conclusions, and significant professional judgments. Paragraph .07: timely basis. Paragraph .17: "After the documentation completion date, the auditor should not delete or discard audit documentation of any nature before the end of the specified retention period. Such retention period, however, should not be shorter than five years from the report release date."
- **SOX Section 302**: CEO/CFO sub-certifications, including disclosure to auditors and audit committee of all significant deficiencies and material weaknesses in ICFR design or operation, and any fraud (whether material or not) involving management or employees with significant ICFR roles.
- **SOX Section 404**: Management's annual ICFR assessment (Section 404(a)) and external auditor attestation for accelerated/large filers (Section 404(b)). SOX 103(a)(2)(A)(i) directs PCAOB to require seven-year audit documentation retention.
- **COSO 2013 Integrated Framework**: five components (Control Environment, Risk Assessment, Control Activities, Information and Communication, Monitoring) and 17 principles.
- **PCAOB Staff Update on 2024 Inspection Activities Spotlight** (March 31, 2025): the most-cited Part I.A deficiency was "did not perform sufficient testing of the design and/or operating effectiveness of controls selected for testing." Most common Part I.B deficiencies in 2024 related to (1) audit committee communications and (2) consideration of fraud.
- **PCAOB AS 1305.04**: written communication of significant deficiencies and material weaknesses to management and the audit committee before the audit report is issued.

# RELATIONSHIP TO QUALITY GATE

The audit trail and Quality Gate are not the same thing.

Audit trail answers: What did we produce, what evidence did we use, and who reviewed it?

Quality Gate answers: Is the output good enough, what did it miss, and what should the finance system learn before the next cycle?

For self-improving finance workflows, produce a Quality Gate & Learning Note first. Produce a formal audit trail entry when the user requests it or when the output is material enough to require formal documentation.

Do not write Learning Candidates to AUDIT.md as approved memory. Learning Candidates become active only after CFO approval and should be written to the configured memory layer.

# WHAT GETS LOGGED

Every meaningful output:

- Board narratives and board memos.
- Covenant memos and lender communications.
- M&A recommendations, walk-away memos, diligence summaries.
- Capital allocation decisions (capex approvals, buyback authorizations, dividend recommendations).
- AI capex justifications and AI vendor term sheets.
- Material weakness disclosures and ICFR remediation plans.
- Earnings call Q&A war-gaming and prepared remarks drafts.
- Scenario forecasts and stress tests.
- Valuation work (DCF, comps, transaction comps).
- 302 certification readiness packages.
- Audit committee pre-meeting briefings.
- Forecast revisions and the rationale for each.

What does NOT get logged:

- Casual explanations or definitional questions.
- Drafts of personal communications.
- Analysis the user explicitly marks as scratch.
- Anything that crosses into legal advice from outside counsel (privilege).

# ENTRY FORMAT

```
## ENTRY [YYYY-MM-DD HH:MM TZ]
Output type: [Board narrative / Covenant memo / M&A recommendation / Capital allocation / AI capex / Material weakness / Earnings Q&A / Scenario forecast / Valuation / 302 readiness / Audit committee briefing / Forecast revision]
Output title: [short title]

Inputs used:
- [Uploaded file name, version, date]
- [Web search performed: query, date, top sources cited]
- [MCP tool called: tool name, query, date]

Sources cited:
- [URL, title, date, page or cell reference]
- [Internal file, sheet, cell]

Confidence grade: [High / Medium / Low]
Reason for grade: [one sentence]

Decision rationale:
- Recommendation: [the bottom line]
- Alternatives considered: [the two or three alternatives]
- Why rejected: [one line per alternative]

Reviewer / sign-off: [user's name and date when accepted]
Sensitive: [Yes / No, default Yes for material weakness, M&A, covenant, comp]
Material event flag: [None / Covenant breach / Material weakness / Going concern / Fraud indicator / Other]
Privilege status: [None / Potentially privileged — outside counsel review recommended]
```

# WHEN CLAUDE WRITES TO [AUDIT.md](http://AUDIT.md)

**Immediately after producing a meaningful output.** Before the user sees the output, the [AUDIT.md](http://AUDIT.md) entry is drafted. The user sees both the output and the entry. The entry is part of the deliverable.

Sequence:

1. User asks for a meaningful output.
2. Claude produces the output.
3. Claude immediately drafts the [AUDIT.md](http://AUDIT.md) entry capturing inputs, sources, confidence, rationale.
4. Claude presents both the output and the entry.
5. The user reviews and signs off (the Reviewer / sign-off field).
6. Entry is appended to [AUDIT.md](http://AUDIT.md).

For web app users: the entry is a copyable code block; the user must paste and re-upload. For Claude Code or Claude in Chrome: auto-write, one-line confirmation.

# SOURCE CITATION REQUIREMENTS

Every quantitative claim, every named entity, every regulatory reference must have a source.

Acceptable:

- URL with title and date.
- Filename, version, sheet, cell, or page reference.
- MCP tool call with query, response timestamp.
- "User-provided in session" with the user message timestamp (only for the user's own assertions).

Not acceptable:

- "From training data" or "general knowledge."
- "Industry consensus" without a named source.
- "It's well known that" — never.

If a claim cannot be sourced, mark it Confidence: Low and Reason for grade: "Inferred from limited evidence; user should verify before acting."

# CONFIDENCE GRADING REQUIREMENTS

**High** requires:

- Primary source (10-K, 10-Q, proxy, official press release, named regulator publication, the user's own data).
- Reasoning robust to obvious counterarguments.
- The decision survives the experienced-auditor reperformance test (per PCAOB AS 1215.06A).

**Medium** requires:

- Credible secondary source (Fortune, WSJ, FT, Bloomberg, named consulting firm publication), or primary source with material uncertainty.
- Reasoning has known weaknesses, named.

**Low** requires:

- Inference from limited evidence.
- Directional guidance only.
- User instruction to verify before acting.

# DECISION RATIONALE REQUIREMENTS

Every recommendation must include:

- The bottom-line recommendation.
- The two or three alternatives considered.
- Why each alternative was rejected.

This is the AICPA AU-C 230.08 standard adapted to CFO work: a person with no previous connection should be able to reconstruct the decision and the path not taken.

# PRIVILEGE BOUNDARIES

Distinguish between:

- **Not privileged:** management analysis, operating decisions, board narratives, capital allocation memos, FP&A work, AI capex justification, earnings prep.
- **Potentially privileged:** legal advice from outside counsel, communications about pending litigation, privileged investigation work product.

If the entry crosses into potentially privileged territory:

- Flag Privilege status: Potentially privileged — outside counsel review recommended.
- Suggest the user route the question to outside counsel before continuing.
- Do not produce a substitute for legal advice.

The skill never replaces outside counsel. Securities counsel, M&A counsel, and SEC enforcement defense counsel are different specialties. When a material event flag fires, name the type of counsel needed.

# MATERIAL EVENT ESCALATION PROTOCOLS

**Covenant breach:**

- Recommend immediate audit committee chair notification.
- Recommend lender notification within the cure window per the credit agreement.
- Recommend banking and securities counsel involvement.
- Note IFRS / GAAP classification implications (current vs. non-current per IAS 1; SOX 302 sub-certification language must reflect the breach if not cured).

**Material weakness:**

- Recommend audit committee chair notification within 48 hours of confirmation.
- Recommend external auditor written communication per PCAOB AS 1305.04.
- Recommend outside counsel drafting of the 10-Q or 10-K disclosure language.
- Re-perform the SOX 302 disclosure controls evaluation.

**Going concern:**

- Recommend audit committee chair, lead independent director, and full board notification.
- Recommend external auditor consultation on the going concern assessment under ASC 205-40.
- Recommend outside counsel and SEC counsel involvement.

**Fraud indicator:**

- Stop. Do not investigate further within the skill.
- Recommend immediate forwarding to general counsel and audit committee chair.
- Reference SOX Section 301 whistleblower obligations.
- Outside counsel must lead the investigation. Do not let management investigate management.

**SEC enforcement risk:**

- Recommend immediate SEC counsel engagement.
- Reference recent enforcement actions: Ammo, Inc. former CFO Robert D. Wiley charged December 15, 2025 (SEC Litigation Release LR-26446) with falsifying books, lying to auditors, and providing false certifications. Ideanomics former CFO Federico Tovar charged April 9, 2024. FAT Brands former CFOs named in SEC complaint May 10, 2024. Kubient former CFO charged September 16, 2024 for fraud and lying to auditors. The pattern: certifications signed without verification, auditor representations made falsely.

# RETENTION AND DISPOSAL

- [AUDIT.md](http://AUDIT.md) is retained for a minimum of seven years from the date of the last entry, aligned with PCAOB AS 1215 audit documentation retention requirements (paragraphs .14-.15) and the SOX statutory minimum (Section 103(a)(2)(A)(i)).
- The AICPA AU-C 230.17 minimum is five years from report release date; the seven-year SOX standard governs for public-company-relevant work.
- After seven years, entries can be archived but should not be destroyed without legal review.
- When the user leaves the company, [AUDIT.md](http://AUDIT.md) is exportable. The user retains a copy as their personal professional record. The company retains a copy for the record of the seat.
- Entries flagged Sensitive or Material event require a 10-year minimum retention.

# EXPORT AND HANDOFF PROCEDURES

When the CFO leaves the company:

1. Export [AUDIT.md](http://AUDIT.md) as a single PDF and a single Markdown file.
2. Index by output type, date, and material event flag.
3. Redact any entries flagged Privilege status: Potentially privileged unless outside counsel approves the disclosure.
4. The successor CFO receives the file as part of the transition. The departing CFO retains a personal copy.
5. The audit committee chair is notified that the file has been transferred.

A clean export is the difference between a graceful exit and a deposition.

# HOW [AUDIT.md](http://AUDIT.md) INTERACTS WITH [MEMORY.md](http://MEMORY.md)

- [AUDIT.md](http://AUDIT.md) is the formal record. Every meaningful output. Sourced. Confidence-graded. Defensible.
- [MEMORY.md](http://MEMORY.md) is the pattern layer. What recurs. What works. What to remember.
- They do not duplicate each other. [AUDIT.md](http://AUDIT.md) captures specific outputs. [MEMORY.md](http://MEMORY.md) captures patterns observed across outputs.
- An [AUDIT.md](http://AUDIT.md) entry may reference a [MEMORY.md](http://MEMORY.md) pattern. A [MEMORY.md](http://MEMORY.md) entry may reference an [AUDIT.md](http://AUDIT.md) output.
- When in doubt, log to [AUDIT.md](http://AUDIT.md). The audit committee respects formal records. Pattern recognition is a private CFO tool.

# STARTER [AUDIT.md](http://AUDIT.md) TEMPLATE

```markdown
# CFO Audit Trail — [Company Name]
Initialized: [YYYY-MM-DD]
Skill: CFO_AUDIT_SKILL.md v2026.05.01
Retention: Minimum seven years from last entry per PCAOB AS 1215 and SOX 103(a)(2)(A)(i).
Privilege framework: Outside counsel review required for any entry flagged Potentially privileged.

---

## ENTRY 2026-04-22 14:30 ET
Output type: Covenant memo
Output title: Q1 2026 Pre-emptive Lender Engagement Memo — First Capital Bank Facility

Inputs used:
- Credit_Agreement_v3_2024-08-15.pdf, Section 7.1(c) leverage definition
- Q1_Forecast_Reforecast_2026-04-15.xlsx, Sheet "Covenant_Math," Cell K42 (4.55x)
- 13_Week_Cash_Forecast_2026-04-21.xlsx, Sheet "Summary"
- Web search 2026-04-22: "covenant waiver vs consent"

Sources cited:
- Credit Agreement Section 7.1(c)
- Internal: Q1 forecast file, 13-week cash forecast, prior year amendment fee precedent

Confidence grade: High
Reason for grade: Primary credit agreement source plus established legal practice on consent vs waiver distinction; supported by directly observed user data.

Decision rationale:
- Recommendation: Engage First Capital Bank lead agent within 7 business days. Request a forward-looking consent for Q3 covenant test, not a retrospective waiver. Lead with the 13-week cash forecast, three cost actions, and sponsor support framework. Target: 25 bps amendment fee, no coupon step-up.
- Alternatives considered:
  1. Wait for Q3 certificate to file and seek waiver after technical breach. Rejected: post-breach negotiating posture is materially weaker; expected fee 50+ bps and likely coupon step-up.
  2. Equity cure ahead of test. Rejected: burns one of three permitted cures and signals weakness to the lender; reserve for liquidity-driven scenarios.
  3. Refinance the facility entirely. Rejected: timing does not allow execution before Q3 test; preserve as a Q4 option if Q3 consent is not granted on acceptable terms.

Reviewer / sign-off: [CFO name, 2026-04-22]
Sensitive: Yes
Material event flag: None (pre-emptive engagement; no breach yet)
Privilege status: None (commercial / management analysis)

---

## ENTRY 2026-04-26 09:15 ET
Output type: M&A recommendation (walk-away memo)
Output title: Project Atlas — Walk-Away Recommendation

Inputs used:
- Project_Atlas_LOI_v4_2026-03-12.pdf
- Atlas_QoE_Report_2026-04-10.pdf (third-party quality of earnings)
- Atlas_Customer_Concentration_Schedule_2026-04-15.xlsx, Sheet "Top10," Cells B5:B14
- Web search 2026-04-26: "current high yield primary new issue spreads B+/B"
- Synergy_Model_v3_2026-04-20.xlsx (with 50% haircut sensitivity)

Sources cited:
- Atlas LOI Section 4 (purchase price and earnouts)
- Atlas QoE Report pages 14-22 (run-rate adjustments)
- Atlas customer concentration: top customer 31% of revenue, top three 58% (2025); contract auto-renewal language has 90-day non-renewal window
- Internal synergy model with $42M run-rate synergies announced; 50% haircut implies $21M; standalone DCF without synergies clears purchase price by negative $87M
- Mauboussin and Rappaport, "Expectations Investing" (revised 2021), SVAR framework for stock deals

Confidence grade: High
Reason for grade: Three independent walk-away triggers fired (customer concentration above policy, QoE found $11M of normalized EBITDA at risk, financing market repriced 75 bps in the last 30 days); standalone math without synergies does not clear at any defensible bid.

Decision rationale:
- Recommendation: Walk away from Project Atlas. Communicate to seller within 5 business days. Preserve relationship for potential future re-engagement at a 25-30% lower price.
- Alternatives considered:
  1. Renegotiate to a lower price. Rejected: customer concentration risk is structural, not price-solvable; even at a 30% lower price the standalone math is marginal.
  2. Restructure to an earnout-heavy deal. Rejected: seller has consistently refused earnout structures in negotiation.
  3. Proceed at current terms with R&W insurance to cover the QoE adjustments. Rejected: R&W insurance does not cover known issues; QoE findings are now known.

Reviewer / sign-off: [CFO name, 2026-04-26]
Sensitive: Yes
Material event flag: None
Privilege status: None (management analysis; deal counsel separately advised on contract mechanics)
```

# THE PCAOB / AICPA REPERFORMANCE TEST

Every entry in [AUDIT.md](http://AUDIT.md) must satisfy this test:

"Could an experienced CFO with no previous connection to the engagement, reading this entry, understand the nature, timing, extent, and results of the work performed; the evidence obtained; the conclusions reached; and identify who performed and reviewed each step?"

If the answer is no, the entry is not done. Add the missing cell, page, source, or rationale. This is the PCAOB AS 1215.06A standard adapted.

# REFERENCES

The skill aligns to and cites:

- PCAOB AS 1215, "Audit Documentation," paragraphs .06, .06A, .08, .09A, .14, .15.
- AICPA AU-C Section 230, "Audit Documentation," paragraphs .07, .08, .17, .18, .19.
- Sarbanes-Oxley Section 302 (15 U.S.C. §7241) — CEO/CFO sub-certifications.
- Sarbanes-Oxley Section 404 (15 U.S.C. §7262) — Management ICFR assessment and external auditor attestation.
- Sarbanes-Oxley Section 103(a)(2)(A)(i) — seven-year audit documentation retention.
- COSO 2013 Internal Control — Integrated Framework, five components and seventeen principles.
- PCAOB Staff Update on 2024 Inspection Activities Spotlight, March 31, 2025.
- PCAOB AS 1305, paragraph .04.