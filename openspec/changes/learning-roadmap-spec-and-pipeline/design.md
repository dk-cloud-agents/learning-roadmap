# Design

## Architecture

```
learning_roadmap.md (source truth: goal, gates, lifecycle)
learning_history.md (source truth: levers)
        │
        ▼
publish_learning_roadmap.py  (reads sources → builds data arrays)
        │
        ▼
learning_roadmap_diagram.html (canonical TEMPLATE — design source of truth)
        │  re.sub data markers
        ▼
learning-roadmap/index.html (GENERATED output, pushed to Pages repo)
```

Two-source model mirrors hung-report exactly: the template is canonical, the
published file is generated output, and a script bridges them on every event.

## Data flow

- `publish_learning_roadmap.py` reads the markdown sources of truth
  (`/opt/data/learning_roadmap.md`, `/opt/data/learning_history.md`).
- Builds the report's mutable values:
  - headline metric (`levers in hand` count + `gates open` count)
  - lifecycle stage statuses
  - lever items (certifications / courses / applied)
  - gates and next-step candidates
- Replaces the corresponding marker blocks in the template
  (`learning_roadmap_diagram.html`) and writes the result to the Pages checkout
  (`/opt/data/learning-roadmap/index.html`).
- Scoped git add of `index.html` only → commit → push. Silent when the
  generated file is byte-identical to the previous commit's (no-op); alert via
  the shared `alert` helper on failure.

## Marker approach

The template keeps a `DATA-MARKER` comment before each mutable block (metric
number, stage status pills, lever rows, gate cards, next steps). The publish
script `re.sub`s between markers, so the layout/CSS/JS stays canonical in the
template and only data varies — never hand-edit the generated file.

## Skill wiring

The ai-learning-coach skill gets a short "published report" subsection:
when D K reports a learning event (course done, cert earned, gate decided),
Lars logs it to the markdown sources **and** runs the publish script in the
same session — mirroring Hung's "on-log publish" trigger in fitness-training-log.

## Git scoping

Same rule as `publish_report.py` (A2): stage ONLY `index.html`. The repo
carries `openspec/` planning files that must never ride along in report
commits.
