# Spec Delta

## MODIFIED Requirements

### Requirement: Open gates and next-step candidates
The report SHALL render a single **Next steps** section: next-step candidates as a numbered list, clearly marked as candidates the learner picks rather than directives. An item that is blocked on a decision (an open gate) SHALL carry an **"Open gate"** label; a plain action SHALL NOT. There is no standalone gates section. Gate-derived items SHALL show their human-readable subject ("Approve cos Sprint 1 …"), never an internal gate code such as "G-learn-1".

#### Scenario: Open gates render
- **WHEN** the next-steps section renders and an item corresponds to an open gate / blocked decision
- **THEN** that item appears with an "Open gate" label using its human-readable subject (no "G-learn-N" code), and no separate gates section is shown

#### Scenario: Next steps render with numbering
- **WHEN** the next-steps section renders
- **THEN** the candidates appear as a numbered list with a supporting hint each, and non-blocked items carry no gate label

### Requirement: Plain-language terms on first use
The report SHALL spell out domain acronyms on first use so a reader unfamiliar with product/agile jargon understands the page without outside knowledge: **PO** → "Product Owner (PO)", **SDD** → "Spec-Driven Development (SDD)", **BDD** → "Behavior-Driven Development (BDD)", and deep agile jargon in visible notes (e.g. "PI progress, DoR checker") SHALL be expressed in plain words ("approvals, progress reporting, readiness checks") rather than raw acronyms. Certificate names (CSM®, CSPO®, SAFe®) remain as-is, optionally with a short qualifier.

#### Scenario: Acronyms are expanded on first use
- **WHEN** a visible section first uses PO, SDD, or BDD
- **THEN** the expansion is given alongside the acronym (e.g. "Product Owner (PO)")

#### Scenario: Deep jargon is translated
- **WHEN** a visible note would show a niche acronym such as "PI progress" or "DoR checker"
- **THEN** it is rendered in plain language ("approvals, progress reporting, readiness checks")