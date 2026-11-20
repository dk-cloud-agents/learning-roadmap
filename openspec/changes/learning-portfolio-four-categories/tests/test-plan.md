# Test Plan — learning-portfolio-four-categories

Approved by D K 2026-11-20 (plan + test-plan gate). Results filled in real in `results.md`. No fabricated passes.

| # | Case | Input / method | Expected outcome |
|---|------|----------------|------------------|
| 1 | Fixture — media counts in metric | Ledger with 1 counted item (Deep Work) | Portfolio metric = 14 (was 13); parked row excluded |
| 2 | Fixture — empty ledger | Consumed table empty | Metric stays 13 (media adds 0); placeholder card renders, no loud failure |
| 3 | Live E2E — 4 cards | Publish; load live URL | Portfolio shows 4 cards (Certifications / Courses / Applied learning / Learning media); Deep Work item inside the grid with date; metric shows portfolio count |
| 4 | Regression | Live page + publish runs | Lifecycle, agentic-core, gates, next-steps intact; publish silent when unchanged; scoped `index.html` commit; mobile no-overflow |