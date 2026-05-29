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

## Motion Reverse Engineering

For URL references that require one-to-one reproduction, inspect motion before implementation and produce a user-confirmable `motion-spec`.

`motion-spec confirmation required` is a hard gate. If live browser reconnaissance fails, stop before final implementation and ask for a screen recording, timestamped screenshots, or explicit approval to approximate.

Observe:

- Initial load at `0s`, `0.5s`, `1s`, `2s`, and `5s`.
- Idle behavior after the page sits untouched.
- Before and after any timed auto-scroll or autoplay transition.
- Automatic-scroll pages: true first screen, just before auto-scroll, just after auto-scroll, and manual return-to-top behavior.
- Key section enter/leave states.
- Hover, click, focus, drag, scroll, resize, and media states.

Record:

- Trigger source: page load, idle timer, scroll threshold, hover, click, focus, drag, media event, section enter, or section leave.
- Timeline: sampled timestamps, delays, loops, cycle duration, and autoplay cadence.
- CSS/JS properties: transform, opacity, filter, blur, scale, rotate, translate, clip-path, mask, z-index, video/canvas/WebGL state, or scroll-timeline behavior.
- Motion path and speed: linear, orbital, radial, vertical, horizontal, parallax, snap, easing feel, direction, transform origin, and acceleration/deceleration.
- Loop behavior: infinite, finite, ping-pong, carousel loop, clamp, pause, resume, and reset.
- Pause/resume conditions: hover pause, pointer leave resume, modal open pause, viewport leave pause, reduced-motion fallback.
- State machine: default, loading, idle, hovering, active, paused, transitioning, section-entered, section-left, completed.
- User confirmation and implementation status: pending, confirmed, implemented, approximated, or gap.
- Failed observations: timeline sampling, hover state, click state, scroll threshold, autoplay, auto-scroll, media, or responsive state.

For the ardot-style hero example, the inventory should be able to describe effects with terms like:

- `ambient orbital rotation`
- `angle-dependent blur filter`
- `hover-triggered 3D flip`
- `hover pauses ambient rotation`
- `initial scale-down entrance animation`
- `timed auto-scroll to next section`
- `section scale-in/scale-out transition`
- `auto-scroll page sampling`

For Ardot-style hero sections, explicitly check orbital rotation, angle-dependent blur, hover-triggered flip, hover pause/resume, initial scale-down entrance, timed auto-scroll, and second-section scale transition.

Do not start one-to-one implementation until the motion behavior is summarized and confirmed by the user, unless the user explicitly chooses to let the agent decide.

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
