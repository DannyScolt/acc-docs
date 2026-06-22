## Why

Phase 5 and Phase 6 now contain much more business content than before, but they still read as large summary blocks rather than layered operational chapters like Phase 1. The document needs another refinement pass so accounting reviewers, BA, dev, and tester teams can navigate each module through smaller subsections, clearer permission boundaries, and tighter use-case-to-rule mapping.

## What Changes

- Refine Phase 5 and Phase 6 in `ACC-noi-dung-nghiep-vu-theo-phase.html` so they follow the same structural reading pattern as Phase 1: main module → smaller subsections / use-case clusters → rules, workflow, and acceptance points that are easier to review and implement.
- Restructure the large Phase 5 invoice and tax sections into more granular internal subsections instead of one large detail table per major heading.
- Restructure the large Phase 6 advanced modules into smaller operational clusters, especially costing, e-banking, and management/reporting content, and add a Phase 6 overall workflow layer.
- Add clearer permission / approval / override coverage where the current text is still too generic, especially for tax closing, payroll visibility, e-banking approvals, and budget controls.
- Tighten the relationship between use cases, workflows, business rules, and acceptance criteria so each cluster is more testable and closer to Phase 1 quality.
- Update OpenSpec requirements to reflect that the issue is no longer missing coverage only, but insufficient structural granularity and implementation readability.

## Capabilities

### New Capabilities
- `phase5-phase1-style-structure`: Requirements for restructuring Phase 5 into smaller Phase-1-style subsections, permission boundaries, and clearer use-case clusters across invoice and tax modules.
- `phase6-phase1-style-structure`: Requirements for restructuring Phase 6 into smaller Phase-1-style subsections, including a Phase 6 overall workflow and more granular treatment of advanced modules.

### Modified Capabilities
- `phase5-einvoice-detail`: Refine the existing Phase 5 e-invoice requirements so major sections are split into smaller operational subsections rather than one large block per module.
- `phase5-tax-declaration-detail`: Refine the existing Phase 5 tax declaration requirements so checklist, declaration, payment, and adjustment flows are broken into clearer review units.
- `phase5-reporting-controls-detail`: Refine Phase 5 workflow, controls, acceptance, and reporting requirements to align with the more granular structure.
- `phase6-asset-allocation-detail`: Refine Phase 6 asset and allocation requirements so subsections and review units more closely match Phase 1 reading patterns.
- `phase6-payroll-costing-detail`: Refine Phase 6 payroll and costing requirements to split large workflows into smaller operational clusters with clearer controls.
- `phase6-loan-contract-ebanking-detail`: Refine Phase 6 loan, contract, and e-banking requirements to add approval, status, and audit structure at a more granular level.
- `phase6-management-reporting-detail`: Refine Phase 6 dashboard, analysis, forecasting, and budget requirements so this area is no longer compressed into one oversized block.
- `general-ledger`: Extend traceability requirements where the more granular structure introduces clearer posting, approval, and period-control checkpoints.

## Impact

- Affected document: `ACC-noi-dung-nghiep-vu-theo-phase.html`
- Affected planning artifacts: `openspec/changes/refine-phase5-phase6-structure-like-phase1/*`
- Affected existing change context: the Phase 5 and Phase 6 detailed-change artifacts remain valid as coverage baselines, but this change will refine their structure to better match the Phase 1 benchmark
- Affected review flow: accountant review, BA decomposition, dev implementation mapping, tester case design, and permission / approval analysis for Phases 5 and 6
