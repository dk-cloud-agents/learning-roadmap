# Learning roadmap: spec + auto-update pipeline

## What & Why

The learning-roadmap report (published to GitHub Pages as
`https://dk-cloud-agents.github.io/learning-roadmap/`) ships WITHOUT an OpenSpec
record and WITHOUT an auto-update pipeline. D K's standing rule is spec-driven
development for every AI project — including report apps (the hung-report app
has `openspec/` in its repo, and this one does not). She flagged both gaps on
2026-11-20: "the specs — why did you skip this?" and "we need to mirror the
automatic updating."

This change adds:
1. The **OpenSpec skeleton** for the learning-roadmap report repo
   (`openspec/` with config + specs for the report surface), matching how
   hung-report's repo carries its own `openspec/`.
2. A **publish/pipeline spec** mirroring hung-report's flow: the published
   `index.html` is GENERATED from the source of truth (the roadmap + history
   markdown + template), never hand-edited; a publish script rebuilds it on
   every learning event D K reports and pushes to the Pages repo.

## What changes

- `openspec/config.yaml` + `openspec/specs/learning-roadmap-report/spec.md`
  — the report's requirements, spec-driven.
- A publish script (mirrors `publish_report.py`): regenerates `index.html`
  from the template `learning_roadmap_diagram.html`, stages ONLY that file,
  commits + pushes. Silent when nothing changed; alerts on failure.
- Skill wiring: the ai-learning-coach skill documents the update flow
  ("D K reports a learning event → log it → publish "), so every Lars session
  follows the same on-event publish pattern.

## Design decisions

- Repo carries its own `openspec/` (like hung-report's `web/openspec`), NOT
  cos-project — cos-project is for the cos persona, not report apps.
- The auto-publish commit stages ONLY `index.html` (scoped add, never `-A`),
  so spec files never ride along in report commits — same rule as
  `publish_report.py`'s scoped add (A2).
- Data comes from the markdown sources of truth (`learning_roadmap.md`,
  `learning_history.md`); the template's data arrays are replaced at publish
  time, mirroring how `publish_report.py` re.subs `const dates`/`const rolling`
  into the hung template.

## Out of scope

- A login/auth layer (D K said she'll buy a domain and put it behind login
  later — future change).
- The cos build itself; this is only the learning-roadmap report app.
