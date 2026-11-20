# Tasks

## Locked plan gate (D K approves this test plan before implementation):

- [x] D K reviews the change artifacts (proposal, spec, design, test plan) on GitHub
- [x] D K approves the plan + test plan — 2026-11-20, "Yes" (asked to close the two flagged gaps: specs + auto-update; both implemented per this change)
- [x] NOTE: approval was by direct order to build ("mirror the specs, mirror the automatic updating") after she flagged the gaps as not ok — the change was authored and validated BEFORE implementation, per SDD. Process slip on the ORIGINAL launch (report published without specs) is owned in proposal.md; this change records the correction.

## Implementation

- [x] Add `openspec/` skeleton to the learning-roadmap repo (config.yaml + specs dir)
- [x] Author `publish_learning_roadmap.py` (reads markdown sources → builds data → re.subs template markers → writes index.html)
- [x] Add DATA-MARKER blocks to the canonical template `learning_roadmap_diagram.html`
- [x] Wire the publish steps (git add index.html scoped → commit → push → alert on failure) into the script
- [x] Document the on-log publish flow in the ai-learning-coach skill

## Tests (after implementation)

- [x] Header: avatar, tagline, metric render; collapse on scroll works — pass (live page)
- [x] Mobile: no horizontal scroll at 390px — pass
- [x] Lifecycle: 4 stages in order with status pills — pass
- [x] Levers: 3 groups with annotations — pass
- [x] Gates + next steps render — pass
- [x] Publish rebuilds after source change; silent when unchanged; stages only index.html — pass (fixture E2E + real repo)
- [x] Live URL serves the updated report after push — pass (curl + browser on deployed page)

## Present results

- [x] Fill `tests/results.md` with real pass/fail + evidence — 11/11 pass, no fabricated results
- [x] Hand D K the live link + test report for acceptance — pending her reply
- [ ] On approval: `openspec archive` + mark accessible — D K approved flipping implementation to done (2026-11-20); archive pending this final sign-off
