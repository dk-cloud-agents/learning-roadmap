# Test Plan — learning-roadmap spec and pipeline

Status legend: **pending** = not yet run · **pass** / **fail** / **NA** = after execution.
Approval gate: D K approves this plan BEFORE implementation starts.

| # | Case | Input → Expected |
|---|------|------------------|
| 1 | Header renders | Open report → header shows avatar placeholder, tagline, headline metric |
| 2 | Header collapses on scroll | Dispatch real scroll event → header height shrinks to slim line, `body[scrolled]` set |
| 3 | No horizontal scroll on mobile | 390px viewport → scrollWidth == clientWidth, no overflowing elements |
| 4 | Lifecycle stages render | Section present → 4 stage cards in order with status pills |
| 5 | Levers render | Section present → 3 cards (Certifications/Courses/Applied), items annotated |
| 6 | Gates + next steps render | Sections present → 2 gate cards with Open badge; 3 numbered next steps |
| 7 | Publish rebuilds after source change | Edit a source data value → run publish script → generated index.html reflects it |
| 8 | Publish silent when unchanged | No source change → run publish script → no output, no commit |
| 9 | Publish stages only index.html | Run publish with openspec files present/untracked → commit touches only index.html |
| 10 | Live URL serves updated report | curl the Pages URL after push → served HTML contains the updated value |
| 11 | Avatar swap-in point exists | Inspect template → avatar slot has a clearly marked placeholder to replace |
