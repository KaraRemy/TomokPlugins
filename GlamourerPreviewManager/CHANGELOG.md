# Changelog

All notable changes to this project will be documented in this file.

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
