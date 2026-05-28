# Requirement Flow

Use this flow after reading all provided materials. Do not ask every question mechanically; ask only for missing details that affect implementation.

Ask one question at a time during startup. Do not send a multi-question checklist as the first response.

Startup order:

1. Ask target platform.
2. If the user wants a full website clone from URL, switch to Website Clone Mode and skip stack selection.
3. Ask technology stack only when Website Clone Mode does not apply.
4. Ask for reference materials only if none were already provided.
5. Ask the single highest-impact missing question after analysis.

Do not default to Vite + React, Next.js, Vue, or any other stack before asking. Recommend a default only after the user asks for advice or says they have no preference.

Exception: in Website Clone Mode, the stack is fixed by `JCodesMore/ai-website-cloner-template`: Next.js + React + TypeScript + Tailwind + shadcn/ui.

## Website Clone Mode

Trigger this mode when the user asks to fully clone/copy/reproduce a URL as a complete website, including all observable routes/pages and interactions.

Do not treat this as a normal high-fidelity frontend task. Use `JCodesMore/ai-website-cloner-template` as the required foundation and follow its `/clone-website <target-url...>` or Codex-compatible clone-website workflow when available.

Confirm only the essentials, one at a time:

- Which URL(s) should be cloned, if not already clear.
- Whether the user owns/has permission to clone the site, if there is risk of impersonation or protected content.
- Whether the goal is exact cloning or style imitation. If style imitation, do not use this mode; use Open Design/style-reference workflow.

Website Clone Mode must cover:

- All observable pages/routes.
- Navigation and link behavior.
- Hover, active, focus, selected, disabled states.
- Click effects, modals, drawers, menus, tabs, accordions, carousels, filters, forms, pagination.
- Scroll behavior, sticky/fixed areas, horizontal overflow, responsive breakpoints.
- Visual tokens, assets, media, typography, spacing, colors, radii, shadows, motion.
- Visual QA and README run instructions.

## 1. Platform and Stack

- Target: Web, mini-program, desktop app, or cross-platform.
- Stack: existing repo stack, React, Vue, Next.js, Vite, WeChat Mini Program, Taro, uni-app, Electron, or Tauri.
- Constraints: package manager, UI library, browser support, mobile support, deployment target.

## 2. References

Accept URLs, screenshots, design files, PRDs, sketches, competitor pages, and existing repositories.

If a design link cannot be accessed, ask for exported screenshots and any interaction notes.

When a URL is provided, inspect it as an interactive reference when tools are available:

- Visual tokens: color, typography, spacing, radius, shadow, density, background, breakpoints.
- Layout: viewport, below-fold content, sticky/fixed elements, scroll containers, responsive changes.
- Interactions: hover, active, focus, selected, disabled, click, modal, drawer, dropdown, tab, carousel, filter, sort, pagination, forms.
- Motion: transitions, easing, hover movement, open/close behavior.
- Content treatment: images, icons, badges, truncation, empty states.

If the user expects exact reproduction, match the reference's style and interactions as closely as allowed. If the user expects style imitation, extract visual attributes and keep the new product's structure/content/brand original.

Classify each reference:

- Exact reproduction target: reproduce structure, visuals, and interactions as closely as allowed.
- Style target: imitate the visual style without copying the original page one-to-one.
- Functional reference: borrow behavior or flow.
- Content reference: borrow information architecture or copy structure.
- Design-system reference: use style rules, tokens, or component patterns.

When a website is a style target, use the Open Design design stage when available. Extract design attributes such as mood, density, typography feel, spacing rhythm, color behavior, component shape, elevation, motion, navigation style, and hierarchy. Confirm what should remain original: brand, content, layout, copy, data, assets, and business flow.

Do not treat Open Design-exported HTML differently from other HTML. Use Open Design-specific context only when `DESIGN.md`, design systems, craft rules, skill examples, project metadata, or artifact notes are available.

## 3. Business Scope

Confirm whether the project needs:

- Login, register, forgot password, logout.
- Guest mode.
- Role permissions.
- Protected routes.
- Personal center or account menu.
- Payment, order, publish, favorite, comment, admin, or audit flows.

Ask about account and permissions when the product contains private data, user actions, management pages, commerce, publishing, or personalization.

For login, registration, permissions, or protected actions, also confirm API/data source:

- Are real auth APIs available now?
- Is there an API document or endpoint contract?
- What is the token/session storage strategy?
- How is current user information loaded?
- How are roles and permissions represented?
- What happens when an unauthenticated user clicks a protected action?

If no real API contract is provided, default to a frontend mock auth flow:

- Provide a mock username/password.
- Login only after the user clicks the login button and credentials match the mock rule.
- Keep API calls behind replaceable service functions or an API module.
- Store mock session state in localStorage, sessionStorage, component state, or the existing app store.
- Document mock credentials, storage, assumptions, and future backend integration points in the generated project's README.

## 4. Pages and Routes

Identify all pages and states:

- Home, list, detail, settings, profile, admin, help.
- Login/register.
- 404, no permission, maintenance.
- Empty, loading, error, success.
- Modal/drawer states that behave like pages.

## 5. Data and Forms

Confirm:

- Static mock data or real API.
- Search, filter, sort, pagination, infinite scroll.
- Required fields, validation, submit result, upload, draft, reset, cancel.
- Loading, empty, error, retry.

## 6. Interactions

Confirm every meaningful click or gesture:

- Buttons, cards, list items.
- Tabs, dropdowns, menus.
- Modals, drawers, popovers.
- Form submit/cancel.
- Batch actions.
- Drag/drop, keyboard shortcuts, right-click menus when relevant.

## 7. Layout, Scroll, and Responsive

Confirm:

- Whole-page scroll or local pane scroll.
- Fixed/sticky header, tab bar, toolbar, sidebar, footer, bottom nav.
- Modal/drawer background scroll behavior.
- Horizontal scroll in tables, tabs, kanban, galleries.
- Desktop, tablet, mobile viewports to verify.

## 8. Confirmation Gate

Before coding, summarize:

- Pages and route map.
- Business flows.
- Click event map.
- Scroll map.
- Layout confirmation HTML plan.
- Open questions.

Proceed only after user confirmation or explicit permission to decide.
