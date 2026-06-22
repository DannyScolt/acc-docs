## Context

The current Phase 5 and Phase 6 rewrites solved the original coverage gap: they now contain actors, coded use cases, workflows, business rules, accounting impact, and richer acceptance sections. However, they still do not read like Phase 1 because the content is packed into a small number of oversized tables. Phase 1 feels clearer because it uses more structural layers: major module → smaller submodules / operational slices → rules and outcomes that can be reviewed one unit at a time.

This refinement change is therefore not about inventing new business domains. It is about improving the structure of existing content so the same coverage becomes easier to read, decompose, approve, implement, and test. The target reader is still the same: accountant reviewers, BA, dev, and tester teams.

## Goals / Non-Goals

**Goals:**
- Make Phase 5 and Phase 6 read more like Phase 1 by increasing structural granularity inside each major heading.
- Replace oversized one-table sections with smaller subsections or clustered blocks that each represent a clearer operational slice.
- Add explicit permission / approval / override structure where it is currently only implied in actors or general rules.
- Tighten use-case-to-rule-to-workflow mapping so each review unit is more testable.
- Introduce a Phase 6 overall workflow layer similar to what Phase 5 already has, so the advanced modules feel like one coherent chapter rather than isolated blocks.

**Non-Goals:**
- Creating entirely new functional scope for Phases 5 and 6 beyond what was already covered in the detailed changes.
- Rewriting Phase 1 itself.
- Changing the business meaning of the modules where the current content is already acceptable; the main objective is structural refinement.
- Implementing runtime logic or application behavior changes.

## Decisions

### 1. Keep the existing Phase 5 and Phase 6 top-level chapter numbers, but increase internal heading depth
The chapter numbers 6.1–6.9 and 7.1–7.8 are already familiar and should remain recognizable. The refinement should happen beneath them by adding smaller internal slices, similar to how Phase 1 uses 2.4.1, 2.4.2, etc.

**Why this approach:**
- It preserves continuity with the accountant-reviewed document.
- It avoids unnecessary renumbering at the chapter level while still improving readability.
- It matches the actual complaint: not missing domains, but insufficient structural layering.

**Alternative considered:** completely renumber all of Phase 5 and 6 from scratch. Rejected because it would create too much churn compared with the value gained.

### 2. Treat oversized sections as clusters of smaller operational units
Sections such as Phase 5 invoice handling, Phase 5 declaration/payment flows, Phase 6 costing, Phase 6 e-banking, and Phase 6 management reporting should be rewritten as multiple smaller operational clusters instead of one oversized table.

**Why this approach:**
- It makes each cluster easier to map to user stories, QA cases, and permission checks.
- It mirrors why Phase 1 feels clearer in practice.
- It reduces the “looks detailed but still hard to implement” problem.

**Alternative considered:** keep the current single-table layout and only add more prose. Rejected because it increases text volume without improving navigability.

### 3. Add a dedicated permission / approval layer to sensitive modules
Modules involving tax close, payroll, e-banking, loans, and budgets need explicit text for who can create, review, approve, override, reopen, or only view. That should be visible inside the module structure, not only as one global rule.

**Why this approach:**
- The user explicitly asked for “đầy đủ từng phân hệ quyền”.
- Sensitive modules are where the current version still feels generic.
- Permission clarity materially affects implementation and testing.

### 4. Add a Phase 6 chapter-level workflow that ties the advanced modules together
Phase 6 currently has strong per-module content but lacks the chapter-level flow that helps the reader understand how the modules relate. The refinement should add a Phase 6 overall operational flow before or alongside the detailed module sections.

**Why this approach:**
- It gives Phase 6 the same chapter-level orientation that Phase 5 gained.
- It makes the advanced modules feel like one chapter, not unrelated add-ons.
- It improves acceptance and traceability reasoning across modules.

### 5. Use existing capability splits, but refine requirements around structural granularity
The current detailed changes already split Phase 5 and Phase 6 by sensible business domains. This refinement should keep those domain boundaries but update the requirement expectations so “detailed” now means “structurally decomposed like Phase 1”, not merely “contains enough bullet points”.

**Why this approach:**
- The existing change set is still a correct baseline for coverage.
- We avoid throwing away valid planning work.
- The new requirement is refinement of presentation and decomposition quality.

## Risks / Trade-offs

- **[Risk] More internal headings make the document longer and visually heavier** → **Mitigation:** keep each subsection focused and avoid duplicating cross-cutting prose that can stay at module or phase level.
- **[Risk] Some modules may be over-decomposed into artificial subsections** → **Mitigation:** split only where the operational differences are meaningful for review, permissions, workflow, or testing.
- **[Risk] Reworking Phase 5 and Phase 6 structure could create numbering drift or broken references** → **Mitigation:** preserve top-level chapter numbering and refine beneath it with careful local structure changes.
- **[Risk] The refined structure may expose places where the current rules are still too generic** → **Mitigation:** capture those gaps explicitly in the new tasks/specs so they can be resolved intentionally instead of hidden inside large summary blocks.
