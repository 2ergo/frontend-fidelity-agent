# Acceptance Checklist

Use this before final response.

## Layout and Visual Fidelity

- If Website Clone Mode was used, the implementation is based on `JCodesMore/ai-website-cloner-template` and uses Next.js + React + TypeScript + Tailwind + shadcn/ui.
- Page hierarchy matches the confirmed layout.
- Spacing, alignment, color, radius, shadow, typography, and density are close to reference.
- Responsive behavior matches confirmed large-screen/tablet/mobile widths.
- Long text, dense content, and narrow widths do not break layout.
- If a reference site was used as a style target, the final UI captures the intended style attributes without copying protected brand assets, exact copy, or distinctive proprietary composition.
- If Open Design or a design system was used, its chosen design constraints are visible in the final UI.
- If a URL was used as an exact reference, visible styling should be deliberately matched: color palette, typography feel, spacing rhythm, radius, shadows, layout density, backgrounds, icons, media treatment, and responsive behavior.

## Interaction Fidelity

- If Website Clone Mode was used, all observable routes/pages, hover states, click effects, overlays, menus, forms, scrolling, responsive states, and motion were inspected and either implemented or explicitly listed as gaps.
- Confirmed clicks work.
- Route transitions, modals, drawers, tabs, dropdowns, and forms behave as confirmed.
- Hover, active, focus, selected, disabled, loading, empty, and error states are implemented where visible or required.
- Animations and transitions match the reference rhythm when feasible.
- If auth is in scope without real APIs, mock login requires a user click, validates documented mock credentials, stores mock session state, supports logout, and keeps API integration behind replaceable service functions.
- If a URL was used as a reference, key hover and click effects from the reference were inspected or explicitly marked as unavailable, then implemented or documented.

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
