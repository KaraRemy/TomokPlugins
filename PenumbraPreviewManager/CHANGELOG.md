# Changelog

All notable changes to this project will be documented in this file.

---

## [1.2.0.0] - 2026-06-05

### Added
- **Mod Option Previews**: Support for adding preview thumbnails to individual mod options within settings groups (both single-select dropdowns and multi-select checkbox lists).
- **Detour ImGui Hook Overlay**: detoured native ImGui calls (`igCheckbox`, `igBeginCombo`, `igSelectable_Bool`, `igSelectable_BoolPtr`) to display a sky-blue FontAwesome icon next to options with previews, showing the tooltip preview instantly on hover.
- **Portability Manifest (ppm.json)**: Individual option preview assignments are tracked in a `ppm.json` manifest and stored inside a `ppm/` folder in the mod's directory, enabling full portability.
- **Sanitized Filenames**: Generated deterministic and human-readable filenames (e.g. `ppm_groupname_optionname_hash.png`) replacing illegal characters to keep mod folder asset structures clean.
- **Consolidated UI Sub-Panel**: Added a "Mod Option Previews" sub-panel below a divider in the main manager window to easily configure individual option previews (pasting clipboard, loading local files, grabbing URLs, and clearing).
- **Unassigned Image Scanner**: Added a section to scan for unassigned images in the `ppm/` folder supporting multiple extensions (`.png`, `.jpg`, `.jpeg`, `.webp`, `.bmp`, `.gif`) with a live thumbnail preview container.
- **Hide Mod List Option**: Added configuration checkbox to completely hide the left mod list column when Penumbra auto-sync is enabled.

### Changed
- Configured size condition to `ImGuiCond.FirstUseEver` to ensure manual resizing of the Preview Manager window persists correctly.

---

## [1.1.0.0] - 2026-06-05

### Added
- **Penumbra Mod Selection Sync**: Automatically switch the active mod in the Preview Manager to match whichever mod you select in Penumbra's UI. Controlled via settings.
- **Configurable Crop Aspect Ratios**: Added support for 4 different crop settings (*No Crop (Preserve Aspect)*, *16:9*, *1:1 (Square)*, and *4:3*) in the settings menu.
- **ImGui File Dialog Integration**: Added a native-styled `Browse...` file picker using Dalamud's built-in `FileDialogManager` (`ImGuiFileDialog`) for local file imports.
- **Inline Action Buttons**: Added setting checkboxes to display quick action buttons (*Paste Clipboard*, *Search XMA*, *Browse File*, *Copy Search Terms*, *Grab from URL*) inside the Penumbra window when no preview is present.
- **Auto-Balancing Button Layout**: Built a dynamic 2-column grid layout for active quick buttons that automatically scales and centers items, stretching odd-numbered final buttons to full-width.
- **In-Game Chat Alerts**: Added red chat log error warnings using the `IChatGui` service for failed or NSFW-restricted inline URL grabs.
- **Interactive URL Popup**: Spawns an input text modal popup inside Penumbra when clicking "Grab from URL" to fetch images on the fly.
- **Aspect Ratio Safe Guards**: Implemented dynamic texture loading guards to prevent division-by-zero layout jiggling when FFXIV loads new graphics.

### Changed
- Replaced the redundant "Add Preview Image" button in the Penumbra window with "Open Preview Manager".
- Renamed all "16:9" hardcoded descriptions in text prompts to dynamically match active cropping configurations.

---

## [1.0.1.0] - 2026-06-05

### Added
- **Real-Time Mod Scans**: Registered to Penumbra's IPC lifecycle events (`ModAdded`, `ModDeleted`, `ModMoved`, `ModDirectoryChanged`) to keep the mod list synchronized automatically.
- **Thread-Safe Scan Queue**: Implemented lock-guarded queuing for background scans to prevent overlapping directory sweeps when fast successive events occur.

---

## [1.0.0.0] - 2026-05-31

### Added
- **Core Release Packaging**: Created automated release script (`publish.py`) to compile, ZIP, copy assets, and update catalog master files (`pluginmaster.json`).
- **Unified Distribution**: Moved binaries to a single repository layout.
- **Metadata Autocomplete**: Added synchronizer to populate descriptions, tags, and icon pointers automatically into the central database.
- **Hygiene & Documentation**: Setup standard `.gitignore` rules for ignore lists and created user manuals.
