# Design

## Context

See `proposal.md` — Why. The report pipeline is fully data-driven: `build_*` functions parse markdown sources and fill `<!--SECTION:name-->` markers. `build_learning_media` already emits a `.lever-card`, so folding it into the portfolio grid is mostly layout/wiring, not new logic. The headline metric is computed in `levers_in_hand()`.

## Goals / Non-Goals

**Goals:**
- Four sibling portfolio cards under one "Learning Portfolio" heading.
- Headline metric counts all four categories (portfolio items), media included.
- Media item count = counted rows in the ledger ($\times$1 each, not parked).

**Non-Goals:**
- No redesign of card visuals (reuse existing `.lever-card` styling).
- The Duolingo-style "nugget / look-forward" element and the accomplished-vs-next filter are explicitly **future iterations** — D K asked to leave them out of this change.
- No new dependencies; no source-column changes.

## Decisions

**D1 — Grid gets a 4th card, no standalone section.** Move the `<!--SECTION:learning_media-->` marker from its own `<section>` into the `.lever-grid` that holds the other three cards. `build_learning_media` already produces a `.lever-card`, so it renders as the 4th child automatically. Rationale: minimal change, matches D K's "same level" mental model.

**D2 — Rename metric + section label.** Template heading "Levers already in hand" → "Learning Portfolio". `levers_in_hand()` is renamed conceptually to the portfolio count = history §1 Completed + roadmap §2 `✅ live` applied + counted ledger rows. Metric label/`metric_goal` text updated to "<N> portfolio items in hand / <G> gates open" (D K approved counting all four). The internal function name may stay or be renamed; behavior is what matters.

**D3 — Media count joins the metric.** `portfolio_count()` adds `len(consumed_ledger_rows)` on top of the existing 13 (certs+courses+applied). Parked rows excluded. Empty ledger adds 0. Rationale: full category parity — a logged media item contributes exactly one, like a lever.

**D4 — Keep the empty-ledger exemption.** The media card with zero counted rows still renders a placeholder card (not a loud failure) and adds 0. Consistent with the previous change.

## Risks / Trade-offs

- **Metric number changes 13 → 14** (with the 1 logged media item) — expected and intended; verified live, and older refs to "13 levers" updated in tests/skill.
- **Section-marker move** could leave a stray removed marker → run `_check_sections`; template edit is a straight move so render verifies.
- **Wording drift** ("levers" vs "portfolio items" appearing inconsistently) → sweep labels in template + script; keep internal fn compatibility.

## Migration Plan

1. Move marker into `.lever-grid`; rename heading + metric text in template.
2. Update metric computation to include media count; wire through existing render path.
3. Fixture + live tests; publish; verify 4 cards + updated metric on live URL.
4. Archive change (sync both delta specs into main specs).

## Open Questions

None that change specs or approach. (Naming of the future "nugget"/look-forward and the past-vs-next filter deferred by D K.)