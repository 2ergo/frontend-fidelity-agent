# Interaction Checklist

Use this checklist to avoid missing behavior hidden behind static UI.

## Full Page Reconnaissance

For URL references and Website Clone Mode, inspect the full page before implementation. Do not rely on only the first viewport.

Cover:

- Top, mid-scroll, bottom, and key sections.
- Large-screen, tablet when relevant, and mobile widths.
- Hover, click, focus, active, scroll, resize, drag, load, submit, and media events.
- Header, hero, nav, section nav, cards, menus, drawers, modals, carousels, forms, media, CTAs, and footer.
- Complex components: carousel, slider, gallery, film strip, product selector, color picker, media viewer, horizontal card rail, tabbed content, comparison rail.
- Scroll-triggered UI changes such as a global header becoming a product nav, sticky capsule bars, CTA reveal/hide, section title pinning, parallax, element scale/fade, lazy loading, and bottom-state changes.

Record an interaction/motion inventory with:

- Page/route and reachable entry.
- Region.
- Trigger.
- Initial state.
- Changed state.
- Motion: duration, easing feel, delay, direction, opacity, translate, scale, rotation.
- Component behavior: controls, pagination, drag/swipe, scroll snap, autoplay/pause, loop/clamp, keyboard/focus, active/disabled states, visible item count, peeking cards, mobile behavior.
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

## Carousels, Galleries, and Sliders

For URL references and Website Clone Mode, inspect every carousel/gallery/slider-like component before implementation.

Record:

- Component type: carousel, gallery, slider, film strip, card rail, media viewer, product selector, or tabbed carousel.
- Items: count, order, visible item count, item dimensions, gaps, peeking/partial cards, media aspect ratios.
- Controls: next/previous buttons, dots, thumbnails, tabs, progress indicators, play/pause, close/open controls.
- Triggers: click, hover, drag, swipe, keyboard arrows/tab/focus, autoplay timer, scroll wheel, touch gestures.
- State: active item, previous/next item, disabled controls, selected dot/thumb/tab, focus ring, hover style.
- Motion: slide/fade/scale, duration, easing feel, momentum, snap behavior, loop or clamp behavior.
- Content behavior: videos autoplay/pause, image lazy-load, captions changing, CTA links per item.
- Responsive behavior: item count, control placement, touch gestures, overflow/scroll snap, mobile fallback.

Implementation must reproduce the discovered behavior or list a gap with the reason. Do not replace an interactive carousel with a static image strip unless the user explicitly approves it.

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
