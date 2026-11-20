# Tasks

## Locked plan gate (D K approves this test plan before implementation):

- [ ] D K reviews the change artifacts (proposal, spec, design, test plan) on GitHub
- [ ] D K approves the plan + test plan

## Implementation

- [ ] Add `openspec/` skeleton to the learning-roadmap repo (config.yaml + specs dir)
- [ ] Author `publish_learning_roadmap.py` (reads markdown sources → builds data → re.subs template markers → writes index.html)
- [ ] Add DATA-MARKER blocks to the canonical template `learning_roadmap_diagram.html`
- [ ] Wire the publish steps (git add index.html scoped → commit → push → alert on failure) into the script
- [ ] Document the on-log publish flow in the ai-learning-coach skill

## Tests (after implementation)

- [ ] Header: avatar, tagline, metric render; collapse on scroll works
- [ ] Mobile: no horizontal scroll at 390px
- [ ] Lifecycle: 4 stages in order with status pills
- [ ] Levers: 3 groups with annotations
- [ ] Gates + next steps render
- [ ] Publish rebuilds after source change; silent when unchanged; stages only index.html
- [ ] Live URL serves the updated report after push

## Present results

- [ ] Fill `tests/results.md` with real pass/fail + evidence
- [ ] Hand D K the live link + test report for acceptance
- [ ] On approval: `openspec archive` + mark accessible
