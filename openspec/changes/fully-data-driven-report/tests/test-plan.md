# Test Plan — fully-data-driven-report

Approved by D K 2026-11-20 (the change plan + test plan gate). Cases below are the acceptance criteria; results are filled in `results.md` with real pass/fail after execution. No fabricated passes.

| # | Case | Input / method | Expected outcome |
|---|------|----------------|------------------|
| 1 | Fixture E2E — add a lever | Edit `learning_roadmap.md` §2: add `| Applied: FIXTURE skill | ✅ live |` | Publish emits the new item in the Applied card AND metric increments by 1; restore source |
| 2 | Fixture E2E — lifecycle status change | Edit §3: `Ship / Operate / Maintain` → `Early` | Lifecycle card re-renders with an `state early` pill |
| 3 | Fixture E2E — gates + metric | Confirm §5 gates render and metric_goal shows `2 gates open` | Two gate cards; metric goal unchanged |
| 4 | Fixture E2E — next-step edit | Edit §4 item 1 text | The new candidate text appears in the next-steps list |
| 5 | Live E2E | Publish real report; load live URL | Every section (lifecycle, agentic-core, levers, gates, next-steps, metric) matches the source-of-truth markdown |
| 6 | No-static check | Inspect the published `index.html` + template | No visible data section content is hardcoded HTML — all emitted by builders; no `<!--SECTION:` leaks into page text |
| 7 | Publish silent when unchanged | Re-run publish with identical sources | Exit 0, no stdout, no new commit |
| 8 | Publish stages only index.html | Inspect the report commit | Scoped `git add -- index.html`; openspec files never ride in it |
| 9 | Regression — header | Live page load | Avatar 120px, tagline, metric 13 render |
| 10 | Regression — collapse on scroll | Scroll past 50px | Header collapses (avatar →40px, header height drops); verified with transitions disabled to read the settled state |
| 11 | Regression — no horizontal scroll | 390px mobile viewport | `scrollWidth == innerWidth`, no overflow |