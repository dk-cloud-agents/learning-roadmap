# Proposal

## Why

D K consumes learning from many *media* — YouTube videos, research papers, blogs, conversations, lectures, TV programs — and wants those to count as learning progress, not just formal courses or applied builds. Today there is no medium-independent record of consumed learning content and no section for it in the Lars report, so this progress goes uncounted. She logs a piece to count it by explicit rule (*"it counts if I log it and ask you to remember it"*), so the report should surface a dedicated, data-driven **Learning media** section.

## What Changes

- Add a **Learning media** section to the published Lars report, driven from a new source of truth `learning_media.md` (medium-independent ledger: date, title, medium, source/link, why it counted).
- Extend the data-driven publish pipeline with a `build_learning_media` section builder + a new `<!--SECTION:learning_media-->` marker in the template — same pattern as lifecycle/levers/gates.
- Add a "Learning media" line item to the roadmap's levers/evidence where appropriate (it is an applied progress signal).
- Non-breaking; no change to existing sections or sources.

## Capabilities

### New Capabilities
- `learning-media`: the medium-independent ledger of consumed learning content (counted-by-logging rule; video/paper/blog/conversation/lecture/TV as a `medium` metadata field) and its rendering in the report.

### Modified Capabilities
*(none — extends the report via a new capability)*

## Impact

- New source: `learning_media.md` (created, 1 counted item + 1 parked-for-review item).
- `publish_learning_roadmap.py` — add `build_learning_media` + register in `SECTIONS`/`BUILDERS`.
- Template `learning_roadmap_diagram.html` — add the section container + marker; small CSS reuse of existing card styles.
- Generated `index.html` (Pages repo) — output only.
- No new dependencies.