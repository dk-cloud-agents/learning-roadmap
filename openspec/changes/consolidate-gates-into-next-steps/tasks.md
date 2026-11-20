# Tasks

## Locked plan gate (D K approves this change's plan + test plan before implementation)

- [ ] D K reviews the change artifacts (proposal, spec, design, task list + test plan)
- [ ] D K approves — nothing below runs before approval
- [ ] After approval: implement, run tests, fill real results, present for acceptance, then archive

## 1. Template

- [ ] 1.1 Remove the standalone **Open gates** `<section>` from `learning_roadmap_diagram.html` (and its `<!--SECTION:gates-->` marker)
- [ ] 1.2 Ensure the Next steps section is the only remaining forward-looking section

## 2. Builder merge

- [ ] 2.1 Update `build_next_steps(roadmap_md)` to read BOTH §5 gates and §6 next steps, merging into one list
- [ ] 2.2 Gate-derived items render with an "Open gate" badge and their HUMAN-READABLE subject (e.g. "Approve cos Sprint 1 …") — never the "G-learn-N" code; §6 plain actions render without a badge
- [ ] 2.3 De-duplicate: if a gate's subject matches a §6 item (e.g. G-learn-1 ≈ "Approve cos Sprint 1"), render it once, badged
- [ ] 2.4 Drop `build_gates`/its section from `SECTIONS` (or mark the gates marker removed) so no gates section is emitted

## 3. Metric (open point from design — D K picks at gate)

- [ ] 3.1 Decide headline metric: keep "<N> portfolio items in hand / <G> gates open" (default) OR drop the gates count. Implement per D K's choice

## 4. Tests (on D K's approved test plan — real results)

- [ ] 4.1 Fixture: gates + next-steps merge into one list; gate item badged with human-readable text (no "G-learn-N"); de-dup removes the §5/§6 duplicate
- [ ] 4.2 Live E2E: publish → single Next steps section, no Open gates section, gate badge visible on the blocked item
- [ ] 4.3 Regression: other sections + portfolio metric intact; publish silent when unchanged; scoped `index.html` commit; mobile no-overflow

## 5. Deliverables

- [ ] 5.1 Fill `test-plan.md` + `results.md` (real pass/fail + evidence) in the change's `tests/`
- [ ] 5.2 Hand D K the live link + test report for acceptance

## Workflow follow-up (after acceptance)

- `openspec archive` the change (+ sync the `learning-roadmap-report` delta into main specs)
- Confirm the live report shows the single Next steps section