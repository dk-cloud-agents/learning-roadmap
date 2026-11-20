# Spec Delta

## MODIFIED Requirements

### Requirement: Open gates and next-step candidates
The report SHALL render a single **Next steps** section: next-step candidates as a numbered list, clearly marked as candidates the learner picks rather than directives. An item that is blocked on a decision (an open gate) SHALL carry an **"Open gate"** label; a plain action SHALL NOT. There is no standalone gates section.

#### Scenario: Open gates render
- **WHEN** the next-steps section renders and an item corresponds to an open gate / blocked decision
- **THEN** that item appears with an "Open gate" label, and no separate gates section is shown

#### Scenario: Next steps render with numbering
- **WHEN** the next-steps section renders
- **THEN** the candidates appear as a numbered list with a supporting hint each, and non-blocked items carry no gate label