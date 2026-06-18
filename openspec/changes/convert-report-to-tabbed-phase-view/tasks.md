# Tasks: Convert ACC Report to Tabbed Phase View

## 1. Prepare HTML Structure
- [x] Add the Tab Navigation HTML block directly below the cover page (or replacing the TOC).
- [x] Wrap or modify existing section blocks (`#overview`, `#phase-1` to `#phase-6`, `#reconciliation`) with `.tab-panel` class.
- [x] Ensure the first tab (Overview or Phase 1) has the `.active` class by default.

## 2. Implement CSS
- [x] Add CSS for the `.tab-nav` and `.tab-btn` elements (professional layout, active states).
- [x] Add CSS for `.tab-panel` (`display: none`) and `.tab-panel.active` (`display: block`).
- [x] Update `@media print` rules to hide `.tab-nav` and force all `.tab-panel` elements to `display: block` with `page-break-before: always`.

## 3. Implement JavaScript
- [x] Add vanilla JS script before `</body>` to handle tab switching logic.
- [x] Ensure clicking a tab updates the `.active` class on both the button and the target panel.
- [x] Smoothly scroll to the top of the content area when a tab is clicked (optional but good UX).

## 4. Verification
- [x] Verify tab switching works correctly without breaking the layout.
- [x] Verify all phase content is preserved.
- [x] Verify print preview (`Cmd+P` / `Ctrl+P`) shows all phases paginated correctly without the tab bar.
