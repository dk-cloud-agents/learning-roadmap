# Proposal

## Why

Today the report is only **partially** generated: the publish script derives the headline metric from markdown, but every other visible section (lifecycle stage cards, agentic-core tags, lever cards, gates, next-steps) is **hand-maintained static HTML** in the template. Editing the source-of-truth markdown (`learning_roadmap.md` §2/§3/§5, `learning_history.md`) alone does NOT update those sections, so the report silently drifts from its source. On 20.11.26 this caused three separate missed updates (new applied levers, PO-buddy under the agentic system, lifecycle stage statuses) — each required a manual template edit on top of the markdown edit. D K rejects the static sections: the report must render entirely from the source of truth.

## What Changes

- **BREAKING (architecture):** the template stops carrying data as hardcoded section HTML. Each data-bearing section becomes a **generation point**: the publish script parses the markdown sources and emits that section's HTML.
- Library-style renderers added to `publish_learning_roadmap.py` for every data section:
  - lifecycle capability map (§3 stages + status pills + notes)
  - agentic-core tags (the "Agentic system" chips)
  - levers-in-hand cards (§2 + history §1 groupings: Certifications / Courses / Applied)
  - open gates (§5)
  - next-step candidates (§6)
  - headline metric (already generated — kept)
- The template keeps all layout + styling; its section containers become empty generation targets (markers) or are built wholesale by the script.
- Editing ANY markdown source becomes the **only** action needed to update the corresponding report section.

## Capabilities

### New Capabilities
*(none — this modifies the existing report capability, no new cohesive system behavior)*

### Modified Capabilities
- `learning-roadmap-report`: the **"Generated artifact from source of truth"** requirement changes from *"the report is generated"* (currently only the metric) to *"every visible data section is generated from markdown"*, so editing markdown alone updates the report and no static section may silently go stale.

## Impact

- `publish_learning_roadmap.py` — significant extension (section builders).
- Template `learning_roadmap_diagram.html` — data sections become generation targets; styling unchanged.
- Generated `index.html` (Pages repo) — output only, never hand-edited.
- No change to sources `learning_roadmap.md` / `learning_history.md` other than what they already carry.
- No new dependencies; pure Python stdlib stays.