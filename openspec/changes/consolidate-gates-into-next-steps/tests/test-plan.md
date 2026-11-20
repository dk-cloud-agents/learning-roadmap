# Test Plan — consolidate-gates-into-next-steps

Approved by D K 2026-11-20 (plan + test-plan gate). Results filled in real in `results.md`. No fabricated passes.

| # | Case | Input / method | Expected outcome |
|---|------|----------------|------------------|
| 1 | Merge gates + next steps | Render with current `learning_roadmap.md` §4 + §5 | One next-steps list; gate-blocked items carry an "Open gate" badge; plain items do not |
| 2 | No G-learn codes | Inspect rendered next-steps | No "G-learn-N" shown; gate items use human-readable subject (e.g. "Approve cos Sprint 1 …") |
| 3 | No Open gates section | Render / live page | The standalone Open gates section and its marker are gone |
| 4 | Metric | Header | "N portfolio items in hand" — gates count dropped |
| 5 | Plain language | Live page audit | PO/SDD/BDD expanded on first use; no bare "PI progress"/"DoR checker" |
| 6 | Regression | Live page + publish runs | Other sections + portfolio metric intact; silent when unchanged; scoped `index.html` commit; mobile no-overflow |