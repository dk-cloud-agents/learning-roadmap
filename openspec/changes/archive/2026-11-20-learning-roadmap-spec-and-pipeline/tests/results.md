# Test Results — learning-roadmap spec and pipeline

Filled with REAL results after execution. Never fabricated.

| # | Case | Status | Evidence |
|---|------|--------|----------|
| 1 | Header renders | **pass** | Browser on live URL 2026-11-20 (re-run after avatar swap): `.top` present, tagline "Your learning roadmap · Lars", metric "9 levers in hand / 2 gates open", avatar renders D K's **real image** (data:image/png base64) at **120px on load** (DOM assert via browser_exec) |
| 2 | Header collapses on scroll | **pass** | Real scroll event (`window.scrollTo(0,300)`, then read state): `body[scrolled]=true`, header height 233px → 60px (browser_exec DOM assert on live page) |
| 3 | No horizontal scroll on mobile | **pass** | 390px mobile viewport (CDP emulation): `scrollWidth==innerWidth==390`, no overflowing elements (programmatic audit, real render) |
| 4 | Lifecycle stages render | **pass** | Live page DOM: `document.querySelectorAll('.stage').length == 4` (Inception/Build/Test/Ship-Maintain, status pills present) |
| 5 | Levers render | **pass** | Live page DOM: 3 `.lever-card` (Certifications/Courses/Applied), items annotated (year/Done/percent/Live/Parked/Awaits) |
| 6 | Gates + next steps render | **pass** | Live page DOM: 2 `.gate` cards with Open badge (G-learn-1, G-learn-2); 3 `.next li` numbered candidates |
| 7 | Publish rebuilds after source change | **pass** | Fixture E2E test (scratch repo, real script): added a Completed cert to fixture history → publish → metric 9→10 in generated index.html, commit made; restore → metric back to 9. Script evidence: `publish_learning_roadmap.py` data build + render assertions |
| 8 | Publish silent when unchanged | **pass** | Real repo run with unchanged sources: script exit 0, stdout empty, git log HEAD unchanged (no commit — asserted before/after) |
| 9 | Publish stages only index.html | **pass** | Fixture commit `git show --stat`: "1 file changed … index.html" only; spec files not in report commit (scoped `git add -- index.html`) |
| 10 | Live URL serves updated report | **pass** | `curl -s https://dk-cloud-agents.github.io/learning-roadmap/` → HTTP 200, served HTML contains "Your learning roadmap · Lars", "PLACEHOLDER", metric; browser verified deployed page (not local file) |
| 11 | Avatar swap-in + sizing | **pass** | Real image is swapped in and sized to match Hung: base rule `width:120px;height:120px` on load, NO mobile shrink to 72px (matches Hung's stays-120 mobile rule), collapses to 40px on scroll. Verified live via `getComputedStyle` (120px→40px) and confirmed no leftover 96/72 width values in served HTML |

All 11 cases executed with real tool output on 2026-11-20 (browser_exec DOM asserts + live curl + git/fixture evidence). No fabricated results.
