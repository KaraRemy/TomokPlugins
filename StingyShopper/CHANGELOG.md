# Changelog - Stingy Shopper

All notable changes to the **Stingy Shopper** plugin will be documented in this file.

---

## [1.0.1.0] - 2026-07-23

### Added
- **Gil Limit Filter**: Added a dynamic `maxGilLimit` filter input field in `MainWindow.cs` to filter lists, hide server categories with no matching items, and dynamically recalculate estimated costs and traveled server counts.
- **World Prioritization**: Added dynamic world lookup (`LocalPlayer?.CurrentWorld`) inside `RegisterPurchase` in `ShoppingListManager.cs`. This prioritizes deducting purchased item quantities from the world the player is currently on.
- **Auto-Sorting**: Implemented dynamic LINQ sorting so that the player's current world is always displayed at the top of the plan UI.
- **Auto-Remove Completed Items**: Added an `AutoRemovePurchasedItems` checkbox in the settings panel to automatically delete items from the active list once they are fully bought (`remaining < 1`).
- **Universalis API Resilience**: Added progressive retries (up to 3 attempts with 2s and 4s delays) to `UniversalisClient.cs` to handle API timeouts, downgrading hard error logs to warnings and showing retry status in the UI bar.

### Fixed
- **Flag Propagation**: Fixed a bug in `ShoppingListManager` to correctly propagate `IsUntradable` and `IsUnlisted` flags to grouped item clones.

---

## [1.0.0.0] - 2026-06-30

### Added
- **Dynamic Optimization Models**:
  - **Maximum Stingy**: Spreads purchase allocations to obtain the absolute cheapest units across all servers.
  - **Balanced**: Relies on a customizable threshold percentage (e.g., 10%) to determine whether traveling to another server is worth the cost.
  - **Maximum Convenience**: Calculates global server costs and groups all purchases to the single cheapest server to minimize travel.
- **Chained World & Market Board Teleportation**:
  - Integrating Lifestream IPC to support chained travel queue commands (e.g., `/li <world> mb`). World hops will automatically transport the player directly to the nearest market board.
  - Adds a context-sensitive **"Go to Market Board"** button in the shopping plan when already on the target world.
- **Clipboard Importer**:
  - Added support for pasting raw Teamcraft lists directly from clipboard.
  - Interactive checkboxes to filter imported items by categories: Pre-crafts, Crystals, Timed Nodes, Gathering, Tomes/Tokens/Scrips, Dungeon/Drops/GC, and Other/Misc.
- **MakePlace Importer**: Support for importing JSON lists exported from MakePlace for housing designs.
- **Chat Purchase Tracker**:
  - Listens to chat messages to automatically decrement remaining items.
  - Uses `SeString` and `ItemPayload` parsing to fetch exact item IDs, guaranteeing that tracking is immune to pluralization (e.g., `"handfuls of magnesia powder"` vs `"magnesia powder"`), language localizations, and format codes.
  - Real-time plan reconstruction automatically updates and removes completed allocations from the UI.
- **Clear Actions**: Added safety modal confirmation to "Clear All" and added a "Clear Completed" button.
- **ImGui Table Enhancements**: Added draggable/resizable column dividers and multi-column sorting headers.
