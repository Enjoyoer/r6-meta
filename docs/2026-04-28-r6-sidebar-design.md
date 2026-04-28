# Design Spec: Sidebar Layout for R6 Attachment Meta

## 1. Goal
Refactor dashboard layout from vertical stack to global sidebar to increase information density and ease of filtering.

## 2. UI/UX Changes
- **Fixed Sidebar (Left)**:
  - Width: ~280px.
  - Contains: Search Input, Category Filter, Muzzle Filter, Grip Filter.
  - Sticky/Fixed position for persistent access.
- **Main Content Area**:
  - Padded container for dashboard items.
  - KPI Grid: Top row.
  - Charts: Middle section (2x2 or responsive grid).
  - Table: Bottom section.
- **Mobile Behavior**:
  - Sidebar becomes top-level collapsible or horizontal scroll group.

## 3. Implementation Details
- **CSS**:
  - Use `display: grid` with `grid-template-columns: 280px 1fr`.
  - Sidebar: `height: 100vh`, `position: sticky`, `top: 0`.
- **HTML**:
  - Wrap existing content in `<div class="app-layout">`.
  - Move filter elements from table section to sidebar.
- **JS**:
  - Ensure existing filter logic works with new DOM locations.

## 4. Visual Style
- Maintain existing dark theme, tokens, and font (Space Grotesk).
- Sidebar: Slightly darker surface (`--color-bg`) or offset (`--color-surface-offset`).
- Modern border-right for separation.
