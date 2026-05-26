# Layout Confirmation HTML Spec

Create `layout-confirmation.html` as a low-fidelity, interactive wireframe for confirming structure and behavior before high-fidelity implementation.

## Required Sections

- Page/state navigation.
- Wireframe preview.
- Interaction notes.
- Scroll behavior notes.
- Open questions.
- Acceptance checklist.

## Wireframe Rules

- Use simple boxes, borders, labels, and neutral colors.
- Represent real layout hierarchy: app shell, header, sidebar, tab bar, main content, footer, modal, drawer, table, list, cards.
- Show fixed or sticky regions with visible labels.
- Do not spend time on final colors, typography, images, or brand visuals.
- Include enough placeholder cards/items/rows to prove scroll behavior.

## Interaction Rules

Every clickable wireframe area should do at least one of:

- Navigate to another wireframe page.
- Toggle a modal, drawer, dropdown, popover, or tab.
- Change a selected/active state.
- Display the event description in an inspector panel.

Use inline `data-action`, `data-target`, or visible labels to make intent inspectable.

## Page and State Coverage

Include pages and states that affect implementation:

- Main routes.
- Important modal/drawer states.
- Empty/loading/error states.
- Auth states when relevant.
- Mobile layout state when materially different.

## User Review Prompt

After generating the file, ask the user to review:

- Are the pages and route transitions correct?
- Does each click do what they expect?
- Are the scrollable regions correct?
- Are fixed/sticky areas correct?
- Are any business flows missing?
