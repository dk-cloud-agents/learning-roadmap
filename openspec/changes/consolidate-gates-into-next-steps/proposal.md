# Proposal

## Why

The report currently has two separate sections — **Open gates** and **Next steps** — that show largely the same things twice (e.g. "G-learn-1: cos Sprint 1 approval" appears in both). D K finds them redundant and unclear ("I don't understand what they're for"). She chose a single **Next steps** section where items that are blocked on a decision carry an **"Open gate"** label, and plain actions don't. This kills the duplication while keeping the "this is waiting on your call" signal.

## What Changes

- **Remove** the standalone **Open gates** section from the report.
- Keep **one "Next steps"** section.
- Items that correspond to an open gate / blocked decision render an **"Open gate"** badge; plain actions render without one.
- The gates themselves remain the source of truth in `learning_roadmap.md` §5 (the roadmap is not deleting the gate *concept* — only its redundant public section).

## Capabilities

### New Capabilities
*(none)*

### Modified Capabilities
- `learning-roadmap-report`: the **"Open gates and next-step candidates"** requirement changes — open gates are no longer rendered as a separate section; instead blocked/next-step items carry an "Open gate" badge. The scenario "Open gates render" is removed/adapted.

## Impact

- Template `learning_roadmap_diagram.html` — remove the Open gates `<section>`; next-steps `<li>` items get an optional badge when their source marks them as a gate/blocked.
- `publish_learning_roadmap.py` — `build_gates` output folds into `build_next_steps` as badges (or the next-steps builder reads §5 gates + §6 next steps); `gates_open()` metric logic may stay or simplify depending on whether the headline metric still counts gates.
- Generated `index.html` — output only.
- `learning_roadmap.md` §5 gates, §6 next steps — unchanged as the data source.

### Open point for design
Whether the headline metric ("N portfolio items in hand / G gates open") keeps the gates count. The metric goal strings reference gates in the header; removing the gates section does not force removing the count from the metric. Will confirm within design/tasks.