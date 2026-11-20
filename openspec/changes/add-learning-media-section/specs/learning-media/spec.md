# Spec Delta

## Purpose

The learning-media ledger is a medium-independent record of learning content D K has consumed and chosen to count — YouTube videos, research papers, blogs, conversations, lectures, TV programs and more — where a piece counts only when she logs it and asks the agent to remember it. The report renders it as a dedicated data-driven section.

## ADDED Requirements

### Requirement: Medium-independent learning-media ledger
The report SHALL maintain a Learning media section listing consumed learning content, where each item carries a `medium` metadata value (video / paper / blog / conversation / lecture / TV / other) rather than the category being the format. Content SHALL count only when D K logs it and asks the agent to remember it (passive consumption does not count).

#### Scenario: Logged item appears in the section
- **WHEN** D K logs a consumed learning item (e.g. a YouTube video) with date and source into the ledger markdown and the publish script runs
- **THEN** the Learning media section renders that item with its date, title, medium, source/link, and why-it-counted note

#### Scenario: Medium-independence
- **WHEN** D K logs items of different media types (video, research paper, blog, conversation, lecture, TV)
- **THEN** all appear in the same section regardless of medium, ordered/grouped only by date or by the medium metadata, never by format-specific subsections

#### Scenario: Parked items are not counted
- **WHEN** an item is saved for review but not yet consumed (parked/inbox)
- **THEN** it does not appear as counted progress; it is kept separate and flagged as not-yet-counted

### Requirement: Data-driven rendering
The Learning media section SHALL be generated from its source-of-truth markdown by the publish script — never hand-edited HTML — matching the fully data-driven report pattern (editing the ledger markdown alone updates the section).

#### Scenario: Ledger edit updates the section
- **WHEN** the ledger markdown changes and the publish script runs
- **THEN** the Learning media section reflects the change without any manual template edit

#### Scenario: Empty ledger renders cleanly
- **WHEN** the ledger has no counted items
- **THEN** the section renders an empty-state (e.g. a quiet placeholder) rather than failing or showing stale content