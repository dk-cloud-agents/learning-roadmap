# Tasks

## Locked plan gate (D K approves this change's plan + test plan before implementation)

- [ ] D K reviews the change artifacts (proposal, spec, design, task list + test plan)
- [ ] D K approves — nothing below runs before approval
- [ ] After approval: implement, run tests, fill real results, present for acceptance, then archive

## 1. Source ledger

- [ ] 1.1 Confirm `learning_media.md` exists at `/opt/data/learning_media.md` with `## Consumed & counted` + `## Parked` tables (one counted item: Deep Work is Over; one parked: Techno Tim)
- [ ] 1.2 Publish pipeline can read the new source: add `MEDIA_MD` path constant

## 2. Section builder

- [ ] 2.1 Add `build_learning_media()` — parse the `## Consumed & counted` table rows (Date | Title | Medium | Source/Link | Why it counted) and emit a card/list; parse `## Parked` rows for the not-counted flag (not emitted as progress)
- [ ] 2.2 Return a quiet empty-state placeholder when the consumed table is empty (spec: "Empty ledger renders cleanly")
- [ ] 2.3 Register `learning_media` in `SECTIONS` and `BUILDERS`; allow it to be exempt from the hard non-empty failure check (empty ledger = valid, renders placeholder)

## 3. Template

- [ ] 3.1 Add a `<!--SECTION:learning_media-->` container in `learning_roadmap_diagram.html`, reusing existing card/list styling

## 4. Tests (on D K's approved test plan — real results, no fabricated passes)

- [ ] 4.1 Fixture: add a logged item to the consumed table → publish → assert it appears in the Learning media section; restore source
- [ ] 4.2 Medium-independence: log items of ≥2 media types → assert all render in the same section
- [ ] 4.3 Parked item does not appear as counted progress
- [ ] 4.4 Live E2E: publish the real report → verify the Learning media section on the live URL shows the Deep Work item with its date
- [ ] 4.5 Regression: other sections + the 13-lever metric unchanged; publish silent when unchanged; scoped `index.html` commit

## 5. Deliverables

- [ ] 5.1 Fill `test-plan.md` + `results.md` (real pass/fail + evidence) in the change's `tests/`
- [ ] 5.2 Hand D K the live link + test report for acceptance

## Workflow follow-up (after acceptance)

- `openspec archive` the change (+ sync the `learning-media` delta spec into main specs)
- Confirm the live report; update roadmap levers/evidence to mention Learning media as a progress signal