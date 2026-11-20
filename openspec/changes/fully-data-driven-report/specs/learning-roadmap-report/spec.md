# Spec Delta

## MODIFIED Requirements

### Requirement: Generated artifact from source of truth
Every visible data section of the published report SHALL be generated from the source-of-truth markdown (`learning_roadmap.md` §2/§3/§5/§6 and `learning_history.md` §1) by the publish script — never from hand-maintained HTML in the template or Pages repo — so that any learning event logged to the markdown sources is reflected in the corresponding report section by running the publish script. Editing a markdown source alone SHALL be sufficient to update the section it drives; no static template section may silently go stale.

#### Scenario: Publish rebuilds the report
- **WHEN** the publish script runs after any source markdown changed
- **THEN** it regenerates the published report from the template + parsed section data and pushes only that file

#### Scenario: Every data section updates from its markdown
- **WHEN** D K logs a change to the source markdown (new lever, changed lifecycle stage status, new agentic-core component, gate, or next-step) and the publish script runs
- **THEN** the corresponding visible section (levers card, lifecycle card, agentic-core tag, gate, next-step list, or headline metric) reflects the change without any manual template edit

#### Scenario: No static data sections remain
- **WHEN** the template is inspected
- **THEN** no visible data-bearing section is hardcoded HTML in the template — every section's content is emitted by a section builder from markdown (styling and layout may remain in the template)

#### Scenario: Publish is silent when unchanged
- **WHEN** the publish script runs and the source data is unchanged
- **THEN** it prints nothing and makes no commit, keeping the cron quiet

#### Scenario: Publish stages only the report file
- **WHEN** the publish script commits
- **THEN** it stages only the report file (scoped add), never the open spec files living beside it