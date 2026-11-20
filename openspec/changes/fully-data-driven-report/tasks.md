# Tasks

## Locked plan gate (D K approves this change's plan + test plan before implementation)

- [ ] D K reviews the change artifacts (proposal, spec, design, this task list + test plan) on GitHub
- [ ] D K approves the plan + test plan — sets the gate for implementation; nothing below runs before this
- [ ] After approval: implement, run the test cases, fill real results, present for D K acceptance, then archive

## 1. Section markers in template

- [ ] 1.1 Add a marker block per data section in `learning_roadmap_diagram.html`: lifecycle, agentic-core tags, levers grid, gates, next-steps (header + headline metric markers already exist) — markers are empty generation containers with a sentinel comment (`<!--SECTION:<name>--> ... <!--/SECTION:<name>-->`), styling/classes kept
- [ ] 1.2 Run `openspec validate --changes` to confirm the change still validates after the template edit (validate is unaffected, but keep it green)

## 2. Section builders in publish script

- [ ] 2.1 Add `build_lifecycle(roadmap_md)` — parse §3 stage rows into (name, status-pill class strong/go/early, note); emit the lifecycle card HTML
- [ ] 2.2 Add `build_agentic_core(roadmap_md)` — emit the agentic-system chips (PO-buddy, cos, second brain, OpenSpec, build/test agents); mark PO-buddy as live
- [ ] 2.3 Add `build_levers(roadmap_md, history_md)` — emit the three cards (Certifications / Courses / Applied) with per-item status annotations from §2 + history §1
- [ ] 2.4 Add `build_gates(roadmap_md)` — emit open-gate cards from §5
- [ ] 2.5 Add `build_next_steps(roadmap_md)` — emit the numbered candidate list from §6
- [ ] 2.6 Wire all builders into `render()` so every marker block is filled from markdown (headline metric path kept as-is)

## 3. Robustness

- [ ] 3.1 Publish fails loudly (non-zero exit + alert) if a required section marker is missing or a builder produces empty output — never emit a silently-empty section
- [ ] 3.2 Keep parsers tolerant: header-anchored so column re-indent/renaming doesn't break them

## 4. Tests (on D K's approved test plan — real results, no fabricated passes)

- [ ] 4.1 Fixture E2E per section: edit ONE source markdown (add a lever / change a stage status / add an agentic-core tag / toggle a gate / add a next-step) → publish → assert the corresponding section emitted reflects the change; restore source
- [ ] 4.2 Live E2E: publish the real report → verify each section on the live URL matches the source-of-truth markdown
- [ ] 4.3 No-static check: inspect the published `index.html` + template — assert no visible data section content is hardcoded (all generated)
- [ ] 4.4 Publish silent when unchanged (exit 0, no commit, stdout empty)
- [ ] 4.5 Publish stages only `index.html` (scoped add) — openspec files never ride in the report commit
- [ ] 4.6 Regression: header (avatar 120px, tagline, metric 13), collapse on scroll, no horizontal scroll at 390px still pass

## 5. Deliverables

- [ ] 5.1 Fill `test-plan.md` + `results.md` (real pass/fail + evidence) in the change's `tests/` dir
- [ ] 5.2 Hand D K the live link + test report for acceptance

## Workflow follow-up (after acceptance)

- `openspec archive` the change (+ sync the delta spec `learning-roadmap-report` into main specs)
- Confirm the live report and update the ai-learning-coach skill to drop the "static sections" pitfall note once refactor lands