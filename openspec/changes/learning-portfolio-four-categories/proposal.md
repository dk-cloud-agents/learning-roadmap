# Proposal

## Why

D K views Certifications, Courses, Applied learning, and (newly) Learning media as **four sibling categories on the same level** — a "Learning Portfolio" of everything she's banked. Today the grid is "Levers already in hand" (three cards) with Learning media as a separate bottom section, and the headline metric counts only "levers" (13) — so logged media is in the report yet not in the number, recreating the very mismatch we fixed. She chose to rename the grid to **Learning Portfolio**, fold media in as the **4th card**, and redefine the headline metric as **"N portfolio items"** counting certs + courses + applied + logged media.

## What Changes

- Rename the report section **"Levers already in hand" → "Learning Portfolio"**.
- Add **Learning media** as a **4th card inside the portfolio grid** (Certifications · Courses · Applied learning · Learning media), replacing the standalone bottom Learning media section.
- Redefine the headline metric to **portfolio items** = completed certs/courses (history §1) + live applied levers (roadmap §2) + **counted learning-media items** (ledger). Metric goal reads "portfolio items in hand / N gates open" (or per D K's approved wording).
- Update the "levers" references in the template/script labels to portfolio language where user-facing.
- Non-breaking data-wise; no change to source tables' columns.

## Capabilities

### New Capabilities
*(none)*

### Modified Capabilities
- `learning-media`: rendering changes from a **standalone section** to a **4th card inside the Learning Portfolio grid**; counted-by-logging rule unchanged.
- `learning-roadmap-report`: the headline metric's meaning changes from "levers in hand" (excludes media) to "portfolio items in hand" (includes counted media), and the grid is renamed "Learning Portfolio".

## Impact

- `publish_learning_roadmap.py` — rename metric/data key; `build_learning_media` emits a `.lever-card` for the grid (already does); `levers_in_hand` → portfolio-count includes media count.
- Template `learning_roadmap_diagram.html` — grid header label → "Learning Portfolio"; metric label text; move the Learning media marker out of its standalone `<section>` into the `.lever-grid`.
- Generated `index.html` (Pages repo) — output only.
- No new dependencies.