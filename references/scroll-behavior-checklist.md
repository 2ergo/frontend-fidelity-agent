# Scroll Behavior Checklist

Use this checklist for layout confirmation and final implementation.

## Identify Scroll Containers

Confirm each container:

- Page body.
- Main content pane.
- Sidebar.
- Top tabs or category strip.
- Table or kanban horizontal area.
- Modal body.
- Drawer body.
- Dropdown menu.
- Mobile bottom-sheet.

## Required Behavior

For each scroll container, record:

- Axis: vertical, horizontal, or both.
- Owner: page, pane, list, table, modal, drawer.
- Height or width constraint.
- Fixed/sticky neighbors.
- Scrollbar visibility expectation.
- Touch behavior on mobile.
- Background scroll behavior while overlays are open.

## Scroll-Driven UI States

For URL references and Website Clone Mode, inspect scroll-driven UI states before implementation.

Record:

- Header variants: initial global nav, compressed nav, product nav, sticky capsule bar, CTA bar, or hidden/revealed header.
- Sticky section states: section title pinning, local nav sticking, tab/category bars sticking.
- CTA changes: buy/explore/contact buttons appearing, disappearing, changing style, or becoming fixed.
- Visual changes: background blur, transparency, shadow, border, radius, height, color, text, icon, or logo changes.
- Motion changes: fade, slide, scale, parallax, section reveal, image/video pinning, lazy-load reveal.
- Thresholds: top, specific pixel offset, entering section, leaving section, midpoint, near bottom.
- Bottom behavior: footer reveal, sticky controls ending, back-to-top, or load-more state.

## Real Scroll Verification

In `layout-confirmation.html`:

- Add enough placeholder content to trigger scroll.
- Verify the intended container scrolls.
- Verify fixed/sticky areas stay in place.
- Verify non-scroll containers do not scroll unexpectedly.
- Verify modal/drawer background scroll matches the intended behavior.
- Verify horizontal scroll areas are actually wider than their viewport.

## Common Questions

Ask the user when unclear:

- Should the whole page scroll or only the content panel?
- Does the sidebar scroll independently?
- Does the header remain fixed?
- Does a tab bar become sticky after scrolling?
- Should a modal lock the background page?
- Is the list paginated, infinite, or virtualized?
- Should mobile use page scroll, internal scroll, or bottom-sheet scroll?
