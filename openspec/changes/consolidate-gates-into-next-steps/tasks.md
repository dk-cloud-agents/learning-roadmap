# Tasks

## Locked plan gate (D K approves this change's plan + test plan before implementation)

- [x] D K reviews the change artifacts (proposal, spec, design, task list + test plan)
- [x] D K approves — nothing below runs before approval
- [x] After approval: implement, run tests, fill real results, present for acceptance, then archive

## 1. Template

- [x] 1.1 Remove the standalone **Open gates** `<section>` from `learning_roadmap_diagram.html` (and its `<!--SECTION:gates-->` marker)
- [x] 1.2 Ensure the Next steps section is the only remaining forward-looking section

## 2. Builder merge

- [x] 2.1 Update `build_next_steps(roadmap_md)` to read BOTH §5 gates and §4 next steps, merging into one list
- [x] 2.2 Gate-derived items render with an "Open gate" badge and their HUMAN-READABLE subject (e.g. "Approve cos Sprint 1 …") — never the "G-learn-N" code; §4 plain actions render without a badge
- [x] 2.3 De-duplicate: if a gate's subject matches a §4 item (e.g. G-learn-1 ≈ "Approve cos Sprint 1"), render it once, badged
- [x] 2.4 Drop `build_gates`/its section from `SECTIONS` (or mark the gates marker removed) so no gates section is emitted

## 3. Metric (open point from design — D K picks at gate)

- [x] 3.1 Decide headline metric: drop the gates count → metric goal = "portfolio items in hand" (D K chose to drop, aligning with the plain-language/removal of the gates section)

## 4. Plain-language terms

- [x] 4.1 Expand acronyms on first use in the visible report: PO → "Product Owner (PO)", SDD → "Spec-Driven Development (SDD)", BDD → "Behavior-Driven Development (BDD)"
- [x] 4.2 Translate deep agile jargon in visible notes (Inception note: "approval, PI progress, DoR checker" → "approvals, progress reporting, readiness checks") into plain words
- [x] 4.3 Keep cert names (CSM®, CSPO®, SAFe®) as-is, optionally adding a short qualifier where it reads naturally

## 5. Tests (on D K's approved test plan — real results)

- [x] 5.1 Fixture: gates + next-steps merge into one list; gate item badged with human-readable text (no "G-learn-N"); de-dup removes the §5/§6 duplicate
- [x] 5.2 Live E2E: publish → single Next steps section, no Open gates section, gate badge visible on the blocked item
- [x] 5.3 Jargon audit: live page shows NO bare "G-learn-N", "PI progress", "DoR checker"; PO/SDD/BDD expanded on first use
- [x] 5.4 Regression: other sections + portfolio metric intact; publish silent when unchanged; scoped `index.html` commit; mobile no-overflow

## 6. Deliverables

- [x] 6.1 Fill `test-plan.md` + `results.md` (real pass/fail + evidence) in the change's `tests/`
- [x] 6.2 Hand D K the live link + test report for acceptance

## Workflow follow-up (after acceptance)

- `openspec archive` the change (+ sync the `learning-roadmap-report` delta into main specs)
- Confirm the live report shows the single Next steps section