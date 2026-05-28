# Interaction Checklist

Use this checklist to avoid missing behavior hidden behind static UI.

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
