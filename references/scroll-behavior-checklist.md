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
- Mini-program `scroll-view`.
- Desktop split pane.

## Required Behavior

For each scroll container, record:

- Axis: vertical, horizontal, or both.
- Owner: page, pane, list, table, modal, drawer.
- Height or width constraint.
- Fixed/sticky neighbors.
- Scrollbar visibility expectation.
- Touch behavior on mobile.
- Background scroll behavior while overlays are open.

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
