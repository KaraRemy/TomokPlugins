# Changelog - Stingy Shopper

All notable changes to the **Stingy Shopper** plugin will be documented in this file.

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
