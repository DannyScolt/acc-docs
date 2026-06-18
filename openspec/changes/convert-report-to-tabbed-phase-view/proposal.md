# Proposal: Convert ACC Report to Tabbed Phase View

## Summary

The current ACC scope document is a long, continuous report that requires heavy scrolling. User feedback indicates this is overwhelming ("ngợp"). This change will convert the layout into a tabbed interface ("1 tab = 1 phase") for easier on-screen reading, while retaining its current CSS capabilities to export nicely to PDF.

## Goals

- **One Tab = One Phase:** Display a top navigation bar allowing users to switch between Overview, Phase 1-6, and Reconciliation.
- **Reduce visual clutter:** Only display the content of the currently selected tab on screen.
- **Maintain single HTML file:** All content, CSS, and JS must live within `ACC-noi-dung-nghiep-vu-theo-phase.html`. No external dependencies or multi-file structures.
- **Preserve Print/PDF behavior:** When printing or exporting to PDF, all phases must be visible and properly paginated (each phase on a new page), ignoring the tab UI.

## Non-goals

- Do not alter the actual business logic, tables, or text content inside each phase.
- Do not introduce external libraries (like React, Vue, jQuery, or Bootstrap). Use vanilla JS and CSS.
