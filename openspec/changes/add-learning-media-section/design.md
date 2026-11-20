# Design

## Context

See `proposal.md` — Why. The Lars report's publish pipeline is now fully data-driven (`publish_learning_roadmap.py`): each visible section is produced by a `build_*` function that parses a markdown source and fills a `<!--SECTION:name-->` marker in the template. This change adds the **Learning media** section on the same pattern, from the new `learning_media.md` ledger.

## Goals / Non-Goals

**Goals:**
- New report section renders every consumed learning item from `learning_media.md`, medium-independent.
- Single source of truth; editing the ledger alone updates the section (reuse of the proven builder+marker mechanism).
- Parked/unconsumed items are held separately and marked not-counted.

**Non-Goals:**
- No redesign of the section visuals beyond reusing existing card/list styles.
- No new dependencies.
- Does not change how courses/certs/applied builds are counted.

## Decisions

**D1 — One ledger file, one builder.** `learning_media.md` uses two tables (`## Consumed & counted`, `## Parked`). `build_learning_media()` reads the file, parses the *Consumed* table rows (Date | Title | Medium | Source/Link | Why it counted), and emits `<li>` items into a card list. Parked rows are parsed for the secondary flag, not emitted as counted progress. Rationale: mirrors the existing `table_rows` helper and keeps one builder per section.

**D2 — Marker + row in `SECTIONS`/`BUILDERS`.** Add a `<!--SECTION:learning_media-->` container in the template (reusing `.lever-card`/list styling) and register the builder like the others. Rationale: the render loop, failure-on-empty check, and scoped-commit path all work unchanged.

**D3 — Source of truth + wiring.** `learning_media.md` sits beside the other markdown sources (`/opt/data/`); the pipeline reads it via `read_md`. No change to the commit contract (scoped `index.html` push; silent when unchanged).

## Risks / Trade-offs

- **Ledger format drift** (columns renamed) → the `table_rows` header-anchored parse is tolerant; a fixture test asserts a logged item appears.
- **Empty ledger** → builder returns a quiet placeholder (per spec "Empty ledger renders cleanly"); `_check_sections` treats a genuinely-empty section as a loud failure only for sections that must be non-empty — the media section is exempted so a fresh ledger still publishes.
- **Non-breaking** → existing sections/sources untouched.

## Migration Plan

1. Land builder + marker; run against a fixture (add a logged item → assert it appears; restore).
2. Publish the real report; verify the Learning media section on the live URL.
3. Confirm the existing 13-lever metric and other sections are unchanged.

## Open Questions

None that change specs or approach.