# Test Results — add-learning-media-section

Filled with REAL results after execution, 2026-11-20. No fabricated passes.

| # | Case | Status | Evidence |
|---|------|--------|----------|
| 1 | Fixture — add a logged item | **pass** | `test_media.py`: added `| 2026-11-12 | Some Research Paper | pdf | arXiv — https://… | read the methods |` → "Some Research Paper" rendered in the section with a `pdf` badge; live ledger untouched |
| 2 | Medium-independence | **pass** | Fixture asserted the added paper and the existing video both render in the same section (one card, medium shown per item as a badge) |
| 3 | Parked not counted | **pass** | Fixture asserted "Techno Tim" is NOT in the rendered section (parked row excluded) |
| 4 | Empty ledger | **pass** | Fixture: consumed table emptied → builder returned the quiet empty-state placeholder ("Nothing logged yet…"); section non-empty, publish valid (empty ledger is not a loud failure) |
| 5 | Live E2E | **pass** | Live URL (browser DOM, cache-busted): "Learning media — consumed & counted" section shows **Deep Work is Over — Benjamin Mateev**, date **2026-11-04**, **YouTube video** badge, clickable link; Techno Tim absent |
| 6 | Regression | **pass** | Live metric = **13**; agentic-core (PO-buddy), levers (Agentic AI, Live), gates (G-learn-1/-2) all intact beside the new section |
| 7 | Silent when unchanged | **pass** | Re-ran publish with unchanged sources: exit 0, no stdout, no commit |
| 8 | Scoped commit | **pass** | Report commit `7d9f5cd`: `1 file changed … index.html (9 insertions)` only |

All 8 cases executed with real tool output on 2026-11-20 (fixture script + live browser DOM asserts + curl/git evidence). No fabricated results.