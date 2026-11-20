# Test Results — learning-portfolio-four-categories

Filled with REAL results after execution, 2026-11-20. No fabricated passes.

| # | Case | Status | Evidence |
|---|------|--------|----------|
| 1 | Fixture — media counts in metric | **pass** | `test_portfolio.py`: `portfolio_items` = **14** with 1 counted media item (13 levers + Deep Work); `media_count` = 1; parked row (Techno Tim) not counted |
| 2 | Fixture — empty ledger | **pass** | `test_portfolio.py`: empty consumed table → `media_count` = 0, portfolio = **13**, builder returns the "Nothing logged yet" placeholder (no loud failure — section non-empty) |
| 3 | Live E2E — 4 cards | **pass** | Live URL (browser DOM): `.lever-card h3` = Certifications · Courses · Applied learning · Learning media; heading renders "LEARNING PORTFOLIO" (CSS uppercases `.sec-label`); header metric = **14**, goal "portfolio items in hand / 2 gates open"; Deep Work item (2026-11-04, YouTube video badge) inside the Learning media card; no standalone "Learning media — consumed" section remains; parked Techno Tim absent |
| 4 | Regression | **pass** | Live: lifecycle (Inception/Build/Test/Ship), agentic-core (PO-buddy, cos…), gates (G-learn-1/-2), next-steps all render; publish re-run silent (exit 0, no stdout, no commit); report commit `35ce80a` scoped to `index.html` only (5 insertions, 11 deletions); 390px emulation no horizontal overflow |

All 4 cases executed with real tool output on 2026-11-20 (fixture script + live browser DOM asserts + git evidence). No fabricated results.