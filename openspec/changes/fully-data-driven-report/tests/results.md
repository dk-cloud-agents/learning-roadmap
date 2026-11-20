# Test Results — fully-data-driven-report

Filled with REAL results after execution, 2026-11-20. No fabricated passes.

| # | Case | Status | Evidence |
|---|------|--------|----------|
| 1 | Fixture E2E — add a lever | **pass** | `test_fixture.py`: added `| Applied: FIXTURE skill | ✅ live |` → `FIXTURE skill` present in generated levers card AND metric 13→14 (`baseline 13 -> 14`); source restored |
| 2 | Fixture E2E — lifecycle status change | **pass** | Fixture: `Ship / Operate / Maintain` → `Early` → generated lifecycle shows `state early` + `Early`; restored back to `In progress` |
| 3 | Fixture E2E — gates + metric | **pass** | Fixture asserted `G-learn-1` + `G-learn-2` in gates section and `metric_goal == 'levers in hand / 2 gates open'` |
| 4 | Fixture E2E — next-step edit | **pass** | Fixture: replaced §4 item 1 with `NEW FIXTURE NEXT STEP` → present in generated next-steps; restored |
| 5 | Live E2E | **pass** | Publish → push → live URL (browser DOM + curl): metric 13, agentic-core shows PO-buddy—live / Second brain—live / cos, levers show Live+Awaits, lifecycle Strong×3 + In progress, gates G-learn-1/-2, next-steps list. All match source |
| 6 | No-static check | **pass** | Template data sections now only `<!--SECTION:name-->` containers (styling kept); published output has NO `<!--SECTION:` in visible text and no hardcoded section content — each filled by its builder |
| 7 | Publish silent when unchanged | **pass** | Re-ran publish with unchanged sources: exit 0, no stdout, git log HEAD unchanged (no commit) |
| 8 | Publish stages only index.html | **pass** | `git show --stat` of report commit: `1 file changed … index.html` only; openspec files only in the propose commit |
| 9 | Regression — header | **pass** | Live: avatar 120px (real image), tagline "Your learning roadmap · Lars", metric 13 |
| 10 | Regression — collapse on scroll | **pass** | Live + transitions disabled (settled state): `body[scrolled]` → avatar 120→40px, `.top` height 256.5→60px. (Raw `getComputedStyle` mid-transition reads 120px — a 0.28s CSS transition settling, NOT a collapse failure; forced-disabled measurement confirms 40px/60px) |
| 11 | Regression — no horizontal scroll | **pass** | 390px CDP emulation: `scrollWidth == innerWidth`, no overflowing elements |

All 11 cases executed with real tool output on 2026-11-20 (fixture scripts + live browser DOM asserts + curl + git evidence). No fabricated results.