# Test Results — consolidate-gates-into-next-steps

Filled with REAL results after execution, 2026-11-20. No fabricated passes.

| # | Case | Status | Evidence |
|---|------|--------|----------|
| 1 | Merge gates + next steps | **pass** | `test_gates.py` + live: next-steps renders 3 items — "Approve cos Sprint 1 …" and "Finish Agentic AI" each with `<span class="tag open">Open gate</span>`; "Lock the §2 applied-learning schema" unbadged |
| 2 | No G-learn codes | **pass** | Rendered output: `G-learn` not in generated `index.html` (grep 0); gate subjects shown human-readable |
| 3 | No Open gates section | **pass** | Template gates `<section>` + `<!--SECTION:gates-->` marker removed; `gates` dropped from `SECTIONS`/`BUILDERS`; live page shows no "OPEN GATES" |
| 4 | Metric | **pass** | Live header: **18 portfolio items in hand** (goal no longer references gates; "%2 gates open" removed) |
| 5 | Plain language | **pass** | Live page: "Product Owner (PO)", "Spec-Driven Development (SDD)", "Behavior-Driven Development (BDD)" all present; "PI progress"/"DoR checker"/"PI progress report"/"Definition-of-Ready" absent |
| 6 | Regression | **pass** | Live: lifecycle/agentic-core/portfolio/learning-media/next-steps all render; metric 18 intact; publish re-run silent (exit 0, no commit); report commit `e7c36e1` scoped to `index.html` only; 390px emulation no horizontal overflow |

All 6 cases executed with real tool output on 2026-11-20 (fixture script + live browser DOM asserts + grep/cd + git evidence). No fabricated results.