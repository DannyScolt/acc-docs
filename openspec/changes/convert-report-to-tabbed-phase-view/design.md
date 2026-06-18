# Design: Convert ACC Report to Tabbed Phase View

## Architecture

The document structure will be updated to act as a Single Page Application (SPA) purely via vanilla HTML/CSS/JS.

1. **Tab Navigation Bar:**
   - A sticky or top-placed navigation container with buttons for each section (Overview, Phase 1, Phase 2, ..., Phase 6, Reconciliation).
   - Each button will have a `data-tab` attribute pointing to the ID of the section it controls.

2. **Content Panels:**
   - Wrap the existing `<section class="report-page">` and `<section class="phase-chapter">` blocks with a new class `.tab-panel`.
   - Add IDs to these panels if they don't have them (e.g., `#tab-overview`, `#tab-phase-1`).

3. **Vanilla JavaScript:**
   - A short script at the end of the `<body>` to handle click events on the tab buttons.
   - The script will remove the `.active` class from all buttons and panels, then add it to the clicked button and its corresponding panel.

4. **CSS State Management:**
   - `.tab-panel { display: none; }`
   - `.tab-panel.active { display: block; }`
   - Style the tab bar to look like modern, professional document tabs.

5. **Print Stylesheet (`@media print`):**
   - `.tab-nav { display: none !important; }` (Hide the tabs when printing)
   - `.tab-panel { display: block !important; page-break-before: always; }` (Force all panels to render, enabling normal PDF pagination)
