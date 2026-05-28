# Interaction Checklist

Use this checklist to avoid missing behavior hidden behind static UI.

## Full Page Reconnaissance

For URL references and Website Clone Mode, inspect the full page before implementation. Do not rely on only the first viewport.

Cover:

- Top, mid-scroll, bottom, and key sections.
- Large-screen, tablet when relevant, and mobile widths.
- Hover, click, focus, active, scroll, resize, drag, load, submit, and media events.
- Header, hero, nav, section nav, cards, menus, drawers, modals, carousels, forms, media, CTAs, and footer.
- Scroll-triggered UI changes such as a global header becoming a product nav, sticky capsule bars, CTA reveal/hide, section title pinning, parallax, element scale/fade, lazy loading, and bottom-state changes.

Record an interaction/motion inventory with:

- Page/route and reachable entry.
- Region.
- Trigger.
- Initial state.
- Changed state.
- Motion: duration, easing feel, delay, direction, opacity, translate, scale, rotation.
- Scroll threshold when relevant.
- Responsive differences.
- Implementation status: implemented, mocked, placeholder, or gap.
- Notes: proprietary media replacement, access limitation, or user confirmation needed.

## Clicks and Navigation

- Buttons.
- Cards.
- List rows.
- Menu items.
- Breadcrumbs.
- Tabs.
- Pagination.
- Back/close icons.

For each, define route, state change, modal/drawer, form submit, toast, or disabled behavior.

For URL references, actively inspect clickable controls when possible. Do not infer every click from static appearance only.

Record:

- Default, hover, active, focus, selected, disabled state.
- Click target or state change.
- Open/close behavior.
- Outside click or escape behavior for overlays.
- Transition/motion behavior.

## Overlays

- Modal.
- Drawer.
- Dropdown.
- Popover.
- Tooltip.
- Bottom sheet.

Confirm open trigger, close trigger, escape/outside click behavior, scroll lock, and focus behavior when relevant.

## Forms

- Required fields.
- Validation timing.
- Disabled submit state.
- Success result.
- Error result.
- Cancel/reset behavior.
- Upload behavior.

## States

- Default.
- Hover.
- Active.
- Focus.
- Selected.
- Disabled.
- Loading.
- Empty.
- Error.
- Success.

## Advanced Interactions

Confirm only when relevant:

- Drag and drop.
- Keyboard shortcuts.
- Right-click menu.
- Multi-select.
- Bulk actions.
- Resizable panes.
- Infinite scroll.
- Pull-to-refresh.
