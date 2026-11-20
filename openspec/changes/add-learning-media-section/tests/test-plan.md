# Test Plan — add-learning-media-section

Approved by D K 2026-11-20 (plan + test-plan gate). Results filled in real in `results.md`. No fabricated passes.

| # | Case | Input / method | Expected outcome |
|---|------|----------------|------------------|
| 1 | Fixture — add a logged item | Add a second row to `## Consumed & counted` in `learning_media.md` | The item renders in the Learning media section; source restored |
| 2 | Medium-independence | Log items of ≥2 media types (e.g. video + a paper) | Both render in the same section, medium shown as a badge |
| 3 | Parked not counted | Confirm `## Parked` row (Techno Tim) | Does NOT appear as counted progress |
| 4 | Empty ledger | Consumed table empty | Section renders a quiet empty-state placeholder, publish still succeeds (not a loud failure) |
| 5 | Live E2E | Publish real report; load live URL | Section shows "Deep Work is Over" with date 2026-11-04 and a YouTube video badge; parked item absent |
| 6 | Regression | Headline metric + other sections | Metric stays 13; agentic-core, levers, gates, next-steps intact |
| 7 | Silent when unchanged | Re-run publish with identical sources | Exit 0, no stdout, no commit |
| 8 | Scoped commit | Inspect report commit | Only `index.html` staged |