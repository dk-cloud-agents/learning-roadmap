# Spec Delta

## MODIFIED Requirements

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

### Requirement: Levers-in-hand summary
The report SHALL list the learner's portfolio as four grouped cards — Certifications, Courses, Applied learning, Learning media — each item annotated with its status, under the heading "Learning Portfolio".

#### Scenario: Three lever groups render
- **WHEN** the portfolio section renders
- **THEN** four cards appear: Certifications, Courses, Applied learning, Learning media

#### Scenario: Each lever shows its status
- **WHEN** a portfolio item renders
- **THEN** it shows the status annotation appropriate to its state (year / Done / percent / Live / Parked / Awaits approval / medium badge)