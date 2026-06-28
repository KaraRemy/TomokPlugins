# Changelog

All notable changes to this project will be documented in this file.

## [1.2.1.0] - 2026-06-28

### Added
- **Middle-Click Preview Zoom Slider**: Added a custom slider under `/ppm settings` allowing users to scale middle-click full-screen zoom overlays from 10% up to 300%.
- **Slash Command Subcommands**: Added `/ppm settings` and `/ppm config` to instantly open the configuration window.
- **Dedicated Documentation & Quick Start**: Added comprehensive `GETTING_STARTED.md` and `FAQ.md` guides to the repository detailing all configuration options and workflows.

### Fixed
- **Multi-Group Option Disambiguation**: Fixed a bug where option names shared across different groups (e.g. `Skirt Textures: Plain` vs `Slide Textures: Plain`) caused image preview collisions in Penumbra. Option resolution now cleanly uses sibling-context matching aligned with Penumbra's rendering pipeline.
- **Static Non-Option Group Filtering**: Automatically hidden static required groups (`Required`, `Required Again`, `Models`) from PPM selectors, matching Penumbra's internal `IsOption` rules for single-option containers.

### Changed
- **Updated Default Configurations**: Updated default settings to `No Crop` for both main and option previews, `Eye / View` icon style, and enabled `Search XMA` and `Hide Mod List` by default.

---

## [1.2.0.9] - 2026-06-27

### Added
- **Support & Community Links**: Added an in-game "Support on Ko-fi" button directly inside the settings window alongside the Support Discord button.

---

## [1.2.0.8] - 2026-06-19

### Added
- **Opt-In Preview Hiding in Penumbra**: Added a setting checkbox `"Hide option previews from Penumbra File Redirections"` under "Integration Options" to programmatically mark option preview images and folders with the system `Hidden` attribute. This recursively hides option previews from Penumbra's "File Redirections" tab to prevent UI clutter while maintaining full portability.
- **Dynamic Hiding/Unhiding Sweeps**: Enabling the setting hides existing option preview directories and files; disabling it removes the `Hidden` attribute to restore standard visibility. Includes helper tooltips clarifying the Windows Explorer behavior.

---

## [1.2.0.7] - 2026-06-12

### Changed
- **Hot-Path Performance Cache**: Added multi-tiered caching for option manifests (`ppm.json`), physical file checks (`File.Exists`), and cache-busted texture paths to eliminate all hot-path disk reads.
- **Active Mod Settings Caching**: Pre-calculated option-to-group mappings and cached active mod details when drawing, eliminating nested linear loops and IPC calls.
- **Unassigned Preview Cache**: Cached unassigned images scanning in the main UI, bypassing redundant directory listings on every frame.

---

## [1.2.0.6] - 2026-06-09

### Fixed
- **Prefix Directory Recognition**: Resolved a folder-scanning bug where mod directories starting with a dot (`.`) or an underscore (`_`) were skipped. Added a targeted blacklist for IDE/VCS directories (like `.git`, `.github`, `.vs`, `.vscode`, `.idea`, and `__MACOSX`) to safely support sorting suffixes and folder names like `.HS`.

---

## [1.2.0.5] - 2026-06-09

### Added
- **Manual Heliosphere Override**: Added a configuration checkbox `"Force PPM previews for Heliosphere mods"` under the settings window to manually force drawing preview images in PPM, with a warning tooltip explaining potential double previews if the Heliosphere plugin is running concurrently.

### Changed
- **Dynamic Heliosphere Detection**: Switched from checking only for a `heliosphere.json` file inside mod folders to checking if the Heliosphere plugin is *actually* active and loaded (via reflection and command checks), resolving issues where users downloaded mods from Heliosphere but did not have the plugin loaded, which caused preview images to not display.
- **Settings Layout Reorganization**: Restructured the settings layout, grouping synchronization and Heliosphere options under a new `"Integration Options"` category header and separator for better visibility, and enlarged the configuration window height to prevent scrollbar clutter.

---

## [1.2.0.4] - 2026-06-08

### Fixed
- **GPose Visibility**: Disabled automatic hiding of the Preview Manager UI during GPose, allowing players to view mod previews while in photo mode.

---

## [1.2.0.3] - 2026-06-06

### Added
- **Selected Option Caching**: Remembers selected settings group and option combinations per mod within the current game session, preventing resetting when navigating between mods.

### Fixed
- **Dalamud Texture Caching (Cache-Busting)**: Redirected temporary cache-busted copies of images to a central system temp directory to resolve native Dalamud texture cache staleness upon crop configuration updates.
- **Mod Directory Preservation**: Added background sweeps that automatically clean up legacy `.ppm_cache_*` files inside mod folders, keeping directory structures 100% clean.
- **Unified Preview Zoom**: Changed the z-zoom key gesture to Middle-Click (holding mouse scroll wheel) for all previews (main mod cards and option icons) to avoid layout conflicts with Penumbra's checkbox right-click context menus.

---

## [1.2.0.2] - 2026-06-05

### Fixed
- **Radio Button Option Previews**: Detoured native `igRadioButton_Bool` and `igRadioButton_IntPtr` calls from `cimgui.dll` to support mod option previews when a settings group has exactly 2 options (which Penumbra renders as radio buttons instead of a dropdown).

---

## [1.2.0.1] - 2026-06-05

### Added
- **In-Game Discord Support Link**: Integrated a direct "Join Support Discord" button in the Settings window.
- **Support Documentation**: Added a dedicated Support & Community section to the plugin's `README.md`.

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
