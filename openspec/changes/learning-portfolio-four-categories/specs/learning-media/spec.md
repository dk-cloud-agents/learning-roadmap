# Spec Delta

## MODIFIED Requirements

### Requirement: Medium-independent learning-media ledger
The report SHALL present learning media as a **card within the Learning Portfolio grid** alongside Certifications, Courses, and Applied learning — each item carrying a `medium` metadata value (video / paper / blog / conversation / lecture / TV / other) rather than the category being the format. Content SHALL count only when D K logs it and asks the agent to remember it (passive consumption does not count), and a counted item SHALL be included in the portfolio-items headline metric.

#### Scenario: Logged item appears in the portfolio card
- **WHEN** D K logs a consumed learning item (e.g. a YouTube video) with date and source into the ledger markdown and the publish script runs
- **THEN** the Learning media card inside the Learning Portfolio renders that item with its date, title, medium, and source; and it is counted in the headline portfolio-items metric

#### Scenario: Medium-independence
- **WHEN** D K logs items of different media types (video, research paper, blog, conversation, lecture, TV)
- **THEN** all appear in the same Learning media card regardless of medium, ordered/grouped only by date or medium metadata, never by format-specific subsections

#### Scenario: Parked items are not counted
- **WHEN** an item is saved for review but not yet consumed (parked/inbox)
- **THEN** it does not appear as counted progress and is excluded from the portfolio-items metric; it is kept separate and flagged as not-yet-counted

### Requirement: Data-driven rendering
The Learning media card SHALL be generated from its source-of-truth markdown by the publish script — never hand-edited HTML — and SHALL render inside the Learning Portfolio grid, matching the fully data-driven report pattern.

#### Scenario: Ledger edit updates the card
- **WHEN** the ledger markdown changes and the publish script runs
- **THEN** the Learning media card reflects the change without any manual template edit

#### Scenario: Empty ledger renders cleanly
- **WHEN** the ledger has no counted items
- **THEN** the card renders an empty-state (e.g. a quiet placeholder) and contributes 0 to the portfolio-items metric, rather than failing or showing stale content