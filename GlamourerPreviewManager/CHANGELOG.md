# Changelog

All notable changes to this project will be documented in this file.

---

## [1.1.0.0] - 2026-06-14

### Added
- **Glamourer Preview Gallery**: A visual browser window (`/gpmgallery` or `/glampreviewgallery`) displaying Glamourer designs in a collapsible category grid. Double-click a card to instantly apply the design.
- **Gallery Image Fit Modes**: Added a toggle option to fit full images inside the card without cropping (Contain) or scale them to fill the card bounds (Cover).
- **Middle-Click Zoom**: Support for holding the middle mouse button on gallery cards to display a full-screen zoomed preview overlay (hiding tooltips during active zoom).
- **Feature Promo Popup**: A one-time onboarding popup window introducing users to the new gallery on startup.

### Changed
- **Tabbed Settings Restructuring**: Organized settings options into distinct tabs (*Previews & Storage*, *Display & UI*, *Screenshot Capture*, and *Information*) for a much cleaner layout.
- **Decoupled Aspect Ratios**: Separated the Gallery card aspect ratio configuration from the screenshot crop overlay ratio, preventing crop setting changes from affecting existing gallery layouts.
- **External Screenshot Watcher Optimization**: Rewrote the directory file watcher to lazily run only when actively in GPM screenshot capture mode, completely avoiding background file system overhead. Added a toggle to automatically delete original screenshots after import.
- **Text Wrapping in Tips**: Refactored the settings information tips to support automatic word-wrapping.

---

## [1.0.1.1] - 2026-06-12

### Changed
- **Design Resolution Cache**: Implemented O(1) Guid and case-insensitive Name lookup dictionaries (`DesignsById`/`DesignsByName`) to eliminate linear sweeps through the designs list on the UI thread.
- **Window Stack Check Optimization**: Cached Glamourer's window state checks, re-evaluating only on window boundary changes to completely avoid linear stack checks inside hooked ImGui button, tree node, and selectable detours.
- **Busted Texture Path Resolver**: Added temp-based cache-busting image copy caching to force Dalamud's texture wrapper to reload updated screenshot and clipboard preview images instantly.

---

## [1.0.1.0] - 2026-06-10

### Fixed
- **Disabled Button Scope Leak**: Resolved a bug where GPM's injected preview buttons (*Paste Clipboard*, *Browse File*, and *Screenshot*) were grayed out and unusable for NPC designs or newly created designs because they were drawn inside Glamourer's `"Export to Dat"` `BeginDisabled` scope.
- **Layout & Position Preservation**: Detoured native `igTableNextColumn` calls to draw the GPM UI immediately after the button row, placing the UI in the correct position but outside of the disabled scope, keeping GPM buttons fully interactive.
- **Hover & Tooltip Flickering**: Implemented a native ImGui window stack (`windowStack`) to track active window names and child window nesting. Added a tooltip/popup guard (`IsTooltipOrPopup`) in `CheckAndDrawDeferredUI()` to prevent tooltip windows from prematurely consuming the deferred UI flag and drawing GPM elements inside tooltip popups, resolving the issue where the GPM UI would briefly hide or flicker when the mouse hovered over the "Export to Dat" button.
- **Icon URL Configuration**: Corrected the incorrect branch path (`/refs/heads/main` to `main`) in the plugin master list and local manifest files to ensure the plugin icon displays properly in the Dalamud plugin installer.

---

## [1.0.0.0] - 2026-06-05

### Added
- **Core Release**: Initial release of Glamourer Preview Manager. Enables attaching preview/cover images to Glamourer designs, pasting from clipboard, browsing files, and taking cropped screenshots directly in-game.
