# Tasks

## Locked plan gate (D K approves this change's plan + test plan before implementation)

- [x] D K reviews the change artifacts (proposal, spec, design, task list + test plan)
- [x] D K approves — nothing below runs before approval
- [x] After approval: implement, run tests, fill real results, present for acceptance, then archive

## 1. Template layout

- [x] 1.1 Move the `<!--SECTION:learning_media-->` marker out of its standalone `<section>` into the `.lever-grid` (becomes the 4th card beside Certifications/Courses/Applied)
- [x] 1.2 Rename the grid section heading "Levers already in hand" → "Learning Portfolio"
- [x] 1.3 Update any "levers" wording visible on the page that should read portfolio (section/hint labels)

## 2. Metric redefinition

- [x] 2.1 Add a media-count to the portfolio metric: count = history §1 Completed + roadmap §2 `✅ live` applied + counted consumed-ledger rows (exclude parked)
- [x] 2.2 Update `metric_goal` text to "<N> portfolio items in hand / <G> gates open" (or approved wording)
- [x] 2.3 Keep empty-ledger semantics: 0 counted media → contributes 0, renders the empty placeholder card (no loud failure)

## 3. Tests (on D K's approved test plan — real results)

- [x] 3.1 Fixture: ledger with 1 counted item → metric counts it (13→14); parked row excluded
- [x] 3.2 Fixture: empty ledger → metric unchanged (media adds 0), placeholder card renders
- [x] 3.3 Live E2E: publish → portfolio shows 4 cards (Certifications/Courses/Applied/Learning media); Deep Work item inside the grid with its date; metric shows the updated portfolio count
- [x] 3.4 Regression: other sections (lifecycle, agentic-core, gates, next-steps) intact; publish silent when unchanged; scoped `index.html` commit; mobile no-overflow

## 4. Deliverables

- [x] 4.1 Fill `test-plan.md` + `results.md` (real pass/fail + evidence) in the change's `tests/`
- [x] 4.2 Hand D K the live link + test report for acceptance

## Workflow follow-up (after acceptance)

- `openspec archive` the change (+ sync `learning-media` + `learning-roadmap-report` delta specs into main specs)
- Note "Learning portfolio" wording in the ai-learning-coach skill; keep the future nugget/look-forward filter parked as a separate iteration.