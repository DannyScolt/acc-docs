# Proposal: Redesign ACC Accounting Scope Document as a Formal PDF Report

## Summary

Redesign the existing single-file HTML document `ACC-noi-dung-nghiep-vu-theo-phase.html` so it reads like a formal business report and exports cleanly to PDF. The document must remain a single HTML file, but each phase should be visually separated as its own report chapter/page to reduce reader fatigue.

## Problem

The current document contains all six implementation phases in one long continuous flow. It now has extensive detail, many tables, and all content is displayed sequentially. This makes it hard for customers, accountants, PMs, and developers to quickly understand the structure or navigate to the phase they care about.

The document is also intended to be printed/exported to PDF, so web-only patterns such as tabs or accordions are not appropriate. The layout should instead use report-style hierarchy, page breaks, summaries, and chapter dividers.

## Goals

- Keep the document as **one HTML file**.
- Make the document feel like a formal report/proposal when exported to PDF.
- Redesign the cover page to look more professional and less like a basic web page.
- Add an executive summary so readers understand the document before reading details.
- Add a table of contents / quick navigation section.
- Make each phase begin on a new page.
- Add a phase intro block for each phase before detailed tables.
- Preserve all existing business content and phase details.
- Improve readability without reducing the level of detail.

## Non-Goals

- Do not split the document into multiple HTML files.
- Do not convert the document into a web app.
- Do not use accordion, tabs, or hidden content as the primary reading pattern.
- Do not rewrite the accounting scope content unless needed for headings/summaries.
- Do not introduce external dependencies, frameworks, or remote assets.

## Proposed Outcome

The document should be structured as:

1. Formal cover page
2. Executive summary
3. Table of contents / quick navigation
4. Overall accounting process summary
5. Phase 1 chapter page + Phase 1 details
6. Phase 2 chapter page + Phase 2 details
7. Phase 3 chapter page + Phase 3 details
8. Phase 4 chapter page + Phase 4 details
9. Phase 5 chapter page + Phase 5 details
10. Phase 6 chapter page + Phase 6 details
11. Periodic reconciliation table
12. Footer

Each phase should read as a standalone chapter inside one PDF.

## Success Criteria

- A reader opening the PDF can understand the whole document from the first 2–3 pages.
- Each phase starts on a new printed/PDF page.
- Phase boundaries are visually clear.
- The cover page looks professional and suitable for customer review.
- The document remains printable on A4.
- All existing phase content remains available.
- HTML structure remains valid after the redesign.
