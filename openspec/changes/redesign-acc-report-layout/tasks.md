# Tasks: Redesign ACC Report Layout

## 1. Review and preserve business content
- [x] Read the current HTML structure and identify the exact boundaries of cover, process overview, phase sections, and reconciliation table.
- [x] Preserve all accounting scope content already written for phases 1–6.

## 2. Redesign the cover page
- [x] Replace the current cover page layout with a more formal report style.
- [x] Remove informal elements (such as emoji-style iconography if still present).
- [x] Add a structured metadata block (phase count, process count, standards reference, version/date).

## 3. Add report front matter
- [x] Add an Executive Summary section after the cover page.
- [x] Add a Table of Contents / Quick Navigation section.
- [x] Ensure both sections render clearly in browser and print output.

## 4. Convert phases into report chapters
- [x] Ensure each phase begins on a new page when printing/exporting PDF.
- [x] Add a dedicated intro block at the start of each phase with objective, scope, and major modules.
- [x] Keep detailed module tables after the phase intro block.

## 5. Improve print/report styling
- [x] Add CSS classes for report pages and page breaks.
- [x] Refine spacing, typography, borders, and summary cards for PDF readability.
- [x] Ensure tables remain printable and do not break awkwardly where possible.

## 6. Validate final output
- [x] Verify the HTML remains structurally valid.
- [x] Review print preview to confirm phase-by-phase pagination.
- [x] Check that the report reads cleanly from cover → summary → TOC → phases → reconciliation.

> Note: Preview server launch in this environment hit a sandbox permission issue with Python `http.server`, so visual browser verification was approximated via HTML structure validation and print-focused CSS/page-break review.
