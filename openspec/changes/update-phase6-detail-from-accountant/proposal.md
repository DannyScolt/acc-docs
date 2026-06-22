## Why

Phase 6 currently lists modules and summary functions, but it does not yet document those modules at the same level of detail as Phase 1. The accountant-facing scope is still too thin for BA, dev, tester, and accounting review because it lacks structured use cases, module-specific business rules, workflows, and accounting traceability.

## What Changes

- Rewrite Phase 6 in `ACC-noi-dung-nghiep-vu-theo-phase.html` from summary tables into Phase-1-style detailed sections while preserving the current 7.1–7.8 module structure.
- Expand the fixed-asset, allocation, payroll, costing, loan, contract, e-banking, dashboard, cash-forecast, and budget content into detailed module specifications with actors, coded use cases, conditions, main flows, results, workflows, and business rules.
- Split the large management/reporting area so dashboard, financial analysis, cash forecasting, and budget controls are described as distinct operational scopes under the existing Phase 6 structure.
- Expand Phase 6 accounting-entry guidance, common rules, deliverables, and acceptance criteria so they can be reviewed and implemented like the existing detailed Phase 1 sections.
- Add OpenSpec requirements that define the expected detail level for each Phase 6 capability and synchronize ledger-impact expectations where Phase 6 modules generate or control accounting postings.

## Capabilities

### New Capabilities
- `phase6-asset-allocation-detail`: Detailed requirements for fixed assets, tools/instruments, prepaid expenses, and periodic allocation workflows in sections 7.1–7.2.
- `phase6-payroll-costing-detail`: Detailed requirements for accounting-focused payroll and production costing workflows in sections 7.3–7.4.
- `phase6-loan-contract-ebanking-detail`: Detailed requirements for loan contracts, commercial contracts, and e-banking operational flows in sections 7.5–7.7.
- `phase6-management-reporting-detail`: Detailed requirements for dashboard, financial analysis, cash-flow forecasting, budget control, Phase 6 common workflows, and acceptance coverage in section 7.8 and the phase-level summary sections.

### Modified Capabilities
- `general-ledger`: Extend ledger-level requirements so depreciation, allocation, payroll, costing, loan interest, repayment, and e-banking-generated postings from Phase 6 remain traceable and consistent with lock-period and source-document rules.

## Impact

- Affected document: `ACC-noi-dung-nghiep-vu-theo-phase.html`
- Affected planning artifacts: `openspec/changes/update-phase6-detail-from-accountant/*`
- Affected business-review scope: fixed assets, CCDC/prepaid expenses, payroll accounting, costing, borrowing, contracts, e-banking, dashboard, financial analysis, cash forecasting, and budgets
- Affected cross-cutting requirements: posting traceability, reconciliation with the general ledger, period locking, role-based permissions, and acceptance criteria for advanced modules
