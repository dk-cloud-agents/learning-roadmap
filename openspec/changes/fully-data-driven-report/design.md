# Design

## Context

See `proposal.md` — Why. The current publish script (`publish_learning_roadmap.py`) only substitutes the headline metric via TWO `DATA-MARKER` blocks in the template; the lifecycle cards, agentic-core tags, lever cards, gates, and next-steps are hardcoded `<div>` HTML in `learning_roadmap_diagram.html`. The script reads `learning_roadmap.md` (rocks) and `learning_history.md` (cert rows). No external deps; pure Python stdlib today.

## Goals / Non-Goals

**Goals:**
- Every visible data section renders from markdown; editing markdown alone updates it.
- Styling/layout stay in the template (light Notion theme already approved — do not redesign).
- Publish contract preserved: scope `index.html`, silent when unchanged, cron-friendly.
- Backward compatible output (same visual sections/classes; consumers and tests unchanged in behavior).

**Non-Goals:**
- No visual/design change. No new dependencies. No change to source markdown schema.
- NOT converting the whole artifact to a server-rendered SPA or build-time templating engine (Jinja/Markdown etc.) — overkill for a static single-page report; marker substitution already proven.

## Decisions

**D1 — Marker-substitution per section (reuse the existing pattern).** Extend `render()` to replace one marker block per data section, exactly like the metric ones already do. Each marker is a sentinel comment (e.g. `<!--SECTION:levers-->...<!--/SECTION:levers-->`). Rationale: zero new infra, matches the tested `DATA-MARKER` mechanism, keeps all CSS/classes in the template. Alternative (wholesale Python-generated HTML) rejected: harder to keep styling in sync and a larger diff for no benefit.

**D2 — Section builders parse the markdown into data, then emit HTML.** Each builder (parse_* → build_*) is a small pure function:
- `build_lifecycle(roadmap_md)` → §3 stages: name, status pill class (strong/go/early), note.
- `build_agentic_core(roadmap_md)` → the agentic-system chips (PO-buddy, cos, second brain, OpenSpec, build/test agents).
- `build_levers(roadmap_md, history_md)` → the three cards (Certifications / Courses / Applied) with per-item status annotations.
- `build_gates(roadmap_md)` → §5 open gates.
- `build_next_steps(roadmap_md)` → §6 candidate list.
- headline metric (existing).
Rationale: functions get the existing fixture E2E testable; the source of truth stays the markdown tables.

**D3 — Data lives in markdown tables as the single home; template sections become empty containers with markers.** After refactor, the template's `.lifecycle`, `.orch-tags`, `.lever-grid`, `.gates`, `.next` inner content is replaced at publish time. The script becomes the only writer of those containers. Rationale: guarantees no static drift — there is literally no hardcoded section content left to forget to update.

**D4 — Keep the scoped commit + silent-when-unchanged contract.** Generate full output, compare to on-disk `index.html`; if identical, stay silent (exit 0). Only on difference: scoped `git add -- index.html`, commit, push. Rationale: preserves cron quietness and the "never hand-edit index.html" rule verified by existing tests.

## Risks / Trade-offs

- **Marker mis-match breaks a whole section** → always validate with `openspec validate` + run the real fixture E2E per section before publish; if a section marker is missing, publish must fail loudly, not emit a silently-empty section.
- **Parsing drift from markdown formatting** (tables re-indent/rename columns) → keep parsers tolerant (header-anchored) and add a fixture test that edits each source type then asserts the emitted section changed.
- **Bigger script** → offset by pure-function design; each builder independently unit-testable.
- **Rollback** → previous `index.html` remains in git history; revert that commit to restore the old (though partially-static) artifact.

## Migration Plan

1. Back up current generated `index.html` (already in git history at the last publish commit).
2. Land builders + markers; run against a fixture repo (add a lever/stage/gate → assert the section changed; restore).
3. Publish the real report; verify each section on the live URL.
4. Keep the rollback commit reference in the archive.

## Open Questions

None that change specs or approach. (CSS class names for status pills are reused as-is; confirmed against template.)