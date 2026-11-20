# learning-roadmap-report Specification

## Purpose

The learning-roadmap report is a public, spec-driven, auto-generated product showing D K's AI-learning journey toward the full-stack agentic PO role — readable on mobile, with a fixed header, lifecycle capability map, levers in hand, open gates, and next steps.

## Requirements

### Requirement: Fixed reporting header with avatar and headline metric
The report SHALL render a fixed header at the top of the page showing a circular coach avatar, a tagline identifying the report owner, and a headline metric summarising current learning state as **portfolio items** (certifications + courses + applied-learnings + counted learning media) over open gates, collapsing to a slim single line when the page is scrolled.

#### Scenario: Header renders with avatar, tagline and metric on load
- **WHEN** the report page loads
- **THEN** a fixed header shows a circular avatar, the tagline, and the headline metric in its expanded state, where the metric reads "<N> portfolio items in hand / <G> gates open" (or approved wording counting all four portfolio categories)

#### Scenario: Header collapses on scroll
- **WHEN** the user scrolls the page past 50px
- **THEN** the header collapses to a single slim line (avatar left, metric right) and stays visible at the top

#### Scenario: No horizontal scroll on mobile
- **WHEN** the report is viewed at a 390px-wide mobile viewport
- **THEN** the document width equals the viewport width and no element overflows horizontally

### Requirement: Lifecycle capability map
The report SHALL present the four product-lifecycle stages (Inception, Build, Test, Ship/Maintain) as cards, each with a name, a status pill (Strong / In progress / Early), and a supporting note.

#### Scenario: Four stages render in order
- **WHEN** the lifecycle section renders
- **THEN** four stage cards appear in order: Inception, Build, Test, Ship/Maintain

#### Scenario: Each stage shows its status
- **WHEN** a stage card renders
- **THEN** the card shows a status pill matching its current progress state and a supporting note

### Requirement: Levers-in-hand summary
The report SHALL list the learner's portfolio as four grouped cards — Certifications, Courses, Applied learning, Learning media — each item annotated with its status, under the heading "Learning Portfolio".

#### Scenario: Three lever groups render
- **WHEN** the portfolio section renders
- **THEN** four cards appear: Certifications, Courses, Applied learning, Learning media

#### Scenario: Each lever shows its status
- **WHEN** a portfolio item renders
- **THEN** it shows the status annotation appropriate to its state (year / Done / percent / Live / Parked / Awaits approval / medium badge)

### Requirement: Open gates and next-step candidates
The report SHALL render open decision gates as cards and next-step candidates as a numbered list, clearly marked as candidates the learner picks rather than directives.

#### Scenario: Open gates render
- **WHEN** the gates section renders
- **THEN** each open gate appears as a card with an Open badge, title, and description

#### Scenario: Next steps render with numbering
- **WHEN** the next-steps section renders
- **THEN** the candidates appear as a numbered list with a supporting hint each

### Requirement: Generated artifact from source of truth
Every visible data section of the published report SHALL be generated from the source-of-truth markdown (`learning_roadmap.md` §2/§3/§5/§6, `learning_history.md` §1, `learning_media.md`) by the publish script — never from hand-maintained HTML in the template or Pages repo — so that any learning event logged to the markdown sources is reflected in the corresponding report section by running the publish script. Editing a markdown source alone SHALL be sufficient to update the section it drives; no static template section may silently go stale.

#### Scenario: Publish rebuilds the report
- **WHEN** the publish script runs after any source markdown changed
- **THEN** it regenerates the published report from the template + parsed section data and pushes only that file

#### Scenario: Every data section updates from its markdown
- **WHEN** D K logs a change to the source markdown (new lever, changed lifecycle stage status, new agentic-core component, gate, next-step, or learning-media item) and the publish script runs
- **THEN** the corresponding visible section (levers card, lifecycle card, agentic-core tag, gate, next-step list, portfolio card, or headline metric) reflects the change without any manual template edit

#### Scenario: No static data sections remain
- **WHEN** the template is inspected
- **THEN** no visible data-bearing section is hardcoded HTML in the template — every section's content is emitted by a section builder from markdown (styling and layout may remain in the template)

#### Scenario: Publish is silent when unchanged
- **WHEN** the publish script runs and the source data is unchanged
- **THEN** it prints nothing and makes no commit, keeping the cron quiet

#### Scenario: Publish stages only the report file
- **WHEN** the publish script commits
- **THEN** it stages only the report file (scoped add), never the open spec files living beside it
