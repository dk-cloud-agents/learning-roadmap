# Design

## Context

See `proposal.md` — Why. The report renders **Open gates** and **Next steps** as two sections that show the same items twice. D K chose one **Next steps** section with an "Open gate" label on blocked items.

## Goals / Non-Goals

**Goals:**
- Single Next steps section (remove standalone Open gates section).
- Items blocked on a decision propagate from roadmap §5 gates into next-steps with an "Open gate" label; plain §6 actions render without one.
- Data stays in `learning_roadmap.md` (§5 gates + §6 next steps) as the single source of truth.

**Non-Goals:**
- No change to the gate *concept* or the roadmap §5 data.
- No redesign of the next-steps styling beyond adding the label.
- No new dependencies.

## Decisions

**D1 — Fold gates into next steps at render time.** `build_next_steps()` reads both §5 gates and §6 next steps. Gate rows become `next` `<li>` items with an "Open gate" badge; §6 rows are plain items. The standalone `build_gates` output is dropped from the template (no `<!--SECTION:gates-->` marker rendered as a section). Rationale: single list, one source each.

**D2 — Remove the gates section from the template** but keep the §5 data in the roadmap markdown (it stays the source D K edits; the report just stops showing it as a separate card). Rationale: matches "remove the redundant section, keep the concept."

**D3 — Headline metric keeps the gates count.** `metric_goal` remains "<N> portfolio items in hand / <G> gates open" — the gate count is still meaningful at a glance even without a list section. Alternative (drop gates from the metric) is a one-line change if D K prefers; flagged at the plan gate.

## Risks / Trade-offs

- **Gate rows may duplicate §6 rows** (e.g. §5 "cos Sprint 1 approval" and §6 "Approve cos Sprint 1") → during the merge, de-duplicate by matching the gate's subject against §6 items so it appears once, badged.
- **Metric reference to gates lingers** → acceptable; the count is still real, sourced from §5.

## Migration Plan

1. Update `build_next_steps` to merge gates (badged) + next steps; remove `build_gates`/gates section from template.
2. Fixture + live tests; publish; verify one section, gate badge present, no duplicate gate mentions.
3. Archive change (sync the `learning-roadmap-report` delta into main specs).

## Open Questions

- Keep or drop the "G gates open" portion of the headline metric? (Design default: keep.)