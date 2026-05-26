# Acceptance Checklist

Use this before final response.

## Layout and Visual Fidelity

- Page hierarchy matches the confirmed layout.
- Spacing, alignment, color, radius, shadow, typography, and density are close to reference.
- Responsive behavior matches confirmed desktop/tablet/mobile widths.
- Long text, dense content, and narrow widths do not break layout.

## Interaction Fidelity

- Confirmed clicks work.
- Route transitions, modals, drawers, tabs, dropdowns, and forms behave as confirmed.
- Hover, active, focus, selected, disabled, loading, empty, and error states are implemented where visible or required.
- Animations and transitions match the reference rhythm when feasible.
- If auth is in scope without real APIs, mock login requires a user click, validates documented mock credentials, stores mock session state, supports logout, and keeps API integration behind replaceable service functions.

## Scroll Fidelity

- Intended scroll containers actually scroll.
- Fixed/sticky regions remain in place.
- Modal/drawer background scroll behavior is correct.
- Horizontal scroll areas work.
- Mobile/touch scroll behavior is checked when relevant.

## Technical Fit

- Existing project conventions are followed.
- No unrelated refactors or style churn.
- Mock data is structured and replaceable.
- Build, lint, or tests are run when available.
- Browser or preview verification is performed when available.
- The project README includes install, development startup, build, preview/start, test/lint/typecheck, environment, and platform-specific run instructions.
- If mock auth or mock APIs are used, the README documents credentials, storage, assumptions, and future integration points.

## Delivery Notes

Report:

- Files changed.
- How to run or open the result.
- Verification performed.
- Any gaps that remain due to missing references, unavailable tools, or unconfirmed behavior.
