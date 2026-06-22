## Context

Phase 6 in `ACC-noi-dung-nghiep-vu-theo-phase.html` is currently organized into the right high-level modules, but each module still stops at summary tables and short descriptions. Compared with the detailed structure already accepted in Phase 1 and the recently expanded Phase 5, Phase 6 still lacks explicit actors, coded use cases, conditions, workflows, module-level business rules, and richer accounting-trace sections.

This design must preserve the current chapter boundaries and existing 7.1–7.8 headings, because those headings already represent the intended module breakdown. The change is therefore a documentation-depth upgrade, not a re-architecture of the phase order. The audience is accounting reviewers, BA, dev, and tester teams who need the Phase 6 scope documented at implementation-ready detail.

## Goals / Non-Goals

**Goals:**
- Upgrade sections 7.1–7.8 to the same review depth already used as the benchmark in Phase 1.
- Keep the existing Phase 6 module structure while rewriting the content under each module into a repeatable detailed format.
- Make each advanced module reviewable through actors, coded use cases, business rules, workflow/state handling, and accounting impact.
- Expand the phase-level accounting-entry table, common rules, delivery outcomes, and acceptance criteria so they cover the newly detailed modules.
- Keep Phase 6 internally consistent with `general-ledger` requirements for posting traceability, source-document linkage, and lock-period behavior.

**Non-Goals:**
- Rewriting Phase 1–5 content.
- Changing the phase sequence or renumbering the existing 7.1–7.8 sections.
- Designing full HRM, treasury, BI, or budgeting products beyond the accounting-focused Phase 6 scope already implied by the document.
- Changing runtime behavior or system code as part of this proposal stage.

## Decisions

### 1. Preserve the current 7.1–7.8 section boundaries and deepen them in place
Phase 6 already has the right macro grouping for this document, so the change will keep the current headings and rewrite the body of each section rather than inventing a new chapter structure.

**Why this approach:**
- It keeps continuity with the document the accountant is already reviewing.
- It matches the successful Phase 5 upgrade pattern: preserve recognizable sections, replace summary-only content with detailed tables.
- It reduces the risk of disturbing neighboring sections or the tabbed layout.

**Alternative considered:** split the management/reporting area into separate top-level sections beyond 7.8. Rejected because it would create unnecessary structural churn; instead, 7.8 will stay as one heading but describe dashboard, analysis, forecasting, and budgeting as distinct operational scopes inside it.

### 2. Split the proposal into four new capabilities plus one ledger delta
The proposal introduces four new capabilities grouped by related business domains and one modified `general-ledger` capability.

- `phase6-asset-allocation-detail` for sections 7.1–7.2
- `phase6-payroll-costing-detail` for sections 7.3–7.4
- `phase6-loan-contract-ebanking-detail` for sections 7.5–7.7
- `phase6-management-reporting-detail` for section 7.8 and the phase-level summary/control sections
- `general-ledger` as the modified cross-cutting capability

**Why this approach:**
- It keeps each spec file reviewable and aligned with real business clusters.
- It avoids one oversized Phase 6 spec while also avoiding too many tiny specs.
- It matches the precedent used for Phase 2 and Phase 5 expansion.

**Alternative considered:** one capability for all of Phase 6. Rejected because the capability would become too broad and harder to review or apply incrementally.

### 3. Use a fixed detailed section template for every rewritten module
Each rewritten Phase 6 module should follow a Phase-1-style structure with these minimum content blocks: Mục tiêu, Actor, Chức năng / Use Case, Điều kiện / dữ liệu đầu vào, Luồng chính, Kết quả, Business Rules, Workflow / trạng thái, Ảnh hưởng kế toán / sổ cái / báo cáo.

**Why this approach:**
- It gives reviewers a predictable format across all advanced modules.
- It makes missing requirements visible immediately.
- It directly addresses the user requirement that later phases be “chi tiết như Phase 1”.

**Alternative considered:** keeping summary tables and only expanding descriptions. Rejected because that still leaves BA/dev/test gaps and does not produce implementation-ready scope.

### 4. Introduce coded use-case and rule prefixes per business cluster
Phase 6 content should use stable prefixes so reviewers can trace modules cleanly:

- `UC-FA-*`, `BR-FA-*` for fixed assets
- `UC-ALLO-*`, `BR-ALLO-*` for CCDC and prepaid allocation
- `UC-PAY-*`, `BR-PAY-*` for payroll accounting
- `UC-COST-*`, `BR-COST-*` for costing
- `UC-LOAN-*`, `BR-LOAN-*` for loan management
- `UC-CONTRACT-*`, `BR-CONTRACT-*` for contracts
- `UC-EBANK-*`, `BR-EBANK-*` for e-banking
- `UC-MGMT-*`, `BR-MGMT-*` for dashboard, analysis, forecasting, and budgets
- `BR-P6-G-*` for Phase 6 common rules

**Why this approach:**
- It mirrors the effective coded pattern already introduced in Phase 5.
- It helps dev/test review module-by-module and rule-by-rule.
- It avoids ambiguous narrative-only requirements in large advanced modules.

**Alternative considered:** plain bullet lists without codes. Rejected because the advanced modules are too broad and need explicit traceability.

### 5. Expand phase-level summary sections, not just module sections
The Phase 6 rewrite must also upgrade the following shared sections:
- `Bảng định khoản mẫu — Giai đoạn 6`
- `Quy tắc nghiệp vụ chung của Giai đoạn 6`
- `Kết quả bàn giao`
- `Tiêu chí nghiệm thu`

These sections should reflect the richer module coverage instead of staying as short summary lists.

**Why this approach:**
- Phase-level controls and acceptance criteria are where cross-module dependencies become reviewable.
- Modules like costing, loans, and e-banking affect posting and reconciliation beyond a single section.
- Phase 5 showed that detailed phase-level controls materially improve review quality.

### 6. Keep HTML implementation constraints simple and safe
When the change is later applied, the HTML rewrite should continue using flat tables and simple section blocks without nested tables.

**Why this approach:**
- It matches the current document’s rendering style.
- It minimizes the chance of breaking the tabbed page structure.
- It keeps preview verification straightforward.

## Risks / Trade-offs

- **[Risk] Phase 6 contains broad domains with many possible variants** → **Mitigation:** document accounting-focused baseline workflows and explicitly note where deeper industry customization remains outside this scope.
- **[Risk] Section 7.8 may become overloaded because it bundles dashboard, analysis, forecasting, and budgets** → **Mitigation:** keep the heading but separate those scopes clearly within the detailed content and in the capability spec.
- **[Risk] E-banking detail can imply operational behavior that depends on bank-specific integrations** → **Mitigation:** describe generic workflows, approval controls, statuses, and traceability requirements rather than bank-specific API mechanics.
- **[Risk] Costing and payroll modules can drift into full ERP/HRM requirements** → **Mitigation:** keep the scope anchored to accounting-facing workflows, postings, controls, and reconciliation only.
- **[Risk] Expanding Phase 6 increases document size significantly** → **Mitigation:** use the standardized two-column detailed table pattern established in prior phases and avoid unnecessary prose.
