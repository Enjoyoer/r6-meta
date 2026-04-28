# Implementation Plan: Sidebar Layout Refactor

## Phase 1: Structure & Styling (HTML/CSS)
- [ ] Create `.app-layout` wrapper in HTML.
  - Verification: Check DOM structure in browser or view file.
- [ ] Implement Sidebar structure `<aside class="sidebar">`.
  - Verification: Sidebar exists in HTML.
- [ ] Move filter controls to sidebar.
  - [ ] Move `#searchInput`, `#catFilter`, `#muzzleFilter` from `.table-controls`.
  - [ ] Add `#gripFilter` to sidebar (new or existing chart filter).
  - Verification: Filters visible in sidebar area.
- [ ] Define Grid Layout in CSS.
  - [ ] `.app-layout { display: grid; grid-template-columns: 280px 1fr; }`
  - [ ] Sidebar: `position: sticky; top: 0; height: 100vh; overflow-y: auto;`
  - [ ] Main: `padding: var(--space-6);`
  - Verification: Layout shows sidebar and main content side-by-side.

## Phase 2: Component Refinement
- [ ] Style Sidebar filters.
  - [ ] Stack selects and input vertically.
  - [ ] Add labels and grouping.
  - Verification: Visual check.
- [ ] Refactor Table Section.
  - [ ] Remove old `.table-controls` if empty.
  - [ ] Adjust table width/scroll.
  - Verification: Table still works and looks good.
- [ ] Refactor KPI & Charts for new width.
  - [ ] Ensure KPI grid is responsive.
  - [ ] Ensure Charts resize correctly.
  - Verification: Resize browser and check.

## Phase 3: Logic & Polish
- [ ] Verify JS event listeners.
  - [ ] Check if moving filters broke any `onchange` or `input` listeners.
  - [ ] Ensure `#gripFilter` logic works globally (optional improvement).
  - Verification: Search and filtering work.
- [ ] Add Mobile Responsive styles.
  - [ ] Hide sidebar/convert to top bar on screens < 900px.
  - Verification: Check on mobile view.

## Final Verification
- [ ] Full end-to-end check of search, filters, charts, and theme toggle.
- [ ] Check for any visual regressions.
