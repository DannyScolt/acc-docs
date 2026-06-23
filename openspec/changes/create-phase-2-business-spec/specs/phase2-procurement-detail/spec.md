## ADDED Requirements

### Requirement: Phase 2 SHALL define the procure-to-pay scope in approved-document form
The standalone Phase 2 document SHALL describe the procurement and accounts payable lifecycle in a normalized format comparable to Phase 1, covering request, purchase order, contract, purchase transaction, vendor invoice, accounts payable, vendor payment, purchase return, purchase discount, and payable reconciliation.

#### Scenario: Procurement modules are fully covered
- **WHEN** a reader reviews the detailed module section of the Phase 2 document
- **THEN** the document SHALL cover the source content for current sections 3.2 through 3.10 with approved-document wording and structure

### Requirement: Procurement transaction content SHALL use the 8-column use case table where appropriate
Business transaction modules in Phase 2 SHALL be expressed with the standardized 8-column use case table used by Phase 1 when the content needs actor, flow, business rule, cross-module linkage, and output visibility.

#### Scenario: Transaction modules are normalized
- **WHEN** a Phase 2 module describes a procurement, payable, payment, return, discount, or reconciliation transaction
- **THEN** that module SHALL use the standardized use case table format instead of duplicated summary and detail blocks

### Requirement: Procurement content SHALL stay consistent with Phase 1 control logic
The Phase 2 document SHALL align payment, approval, posting, and cross-reference wording with the already-approved Phase 1 treatment of cash, bank, and general-ledger behavior.

#### Scenario: Vendor payment links to Phase 1 controls
- **WHEN** a reader reviews vendor payment or payable adjustment behavior in Phase 2
- **THEN** the document SHALL clearly relate those flows to Phase 1 cash, bank, and posting controls without redefining contradictory rules
