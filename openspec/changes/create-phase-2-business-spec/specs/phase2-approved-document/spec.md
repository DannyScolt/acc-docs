## ADDED Requirements

### Requirement: Phase 2 SHALL be published as an independent approved document
The project SHALL provide a standalone HTML file for the approved Phase 2 business specification so users do not need to read Phase 2 only from the aggregated multi-phase source file.

#### Scenario: Standalone file is created
- **WHEN** the change is implemented
- **THEN** the repository SHALL contain `ACC-dac-ta-nghiep-vu-phase-2.html` as a self-contained document at the project root

### Requirement: Phase 2 SHALL inherit the approved presentation framework from Phase 1
The standalone Phase 2 document SHALL use the same approved presentation model as Phase 1, including cover style, letterhead, page-ready layout, section hierarchy, and table/schematic styling, unless Phase 2 content requires clearly justified variation.

#### Scenario: Visual and structural parity is preserved
- **WHEN** a reader compares the Phase 2 document with `ACC-dac-ta-nghiep-vu-phase-1.html`
- **THEN** the Phase 2 document SHALL present the same document conventions for letterhead, section framing, tables, and self-contained printable formatting

### Requirement: Phase 2 SHALL include the same top-level documentation layers as Phase 1
The standalone Phase 2 document SHALL be organized into overview, shared control flow, detailed module specification, and appendix sections so readers can move from scope to control rules to detailed business behavior.

#### Scenario: Required document layers are present
- **WHEN** a reader opens the standalone Phase 2 file
- **THEN** the document SHALL include a scope overview section, a common document-state section, a detailed module section, and appendix material for business rules, accounting entries, handover outcomes, and acceptance criteria
