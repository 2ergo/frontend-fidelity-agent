# Requirement Flow

Use this flow after reading all provided materials. Do not ask every question mechanically; ask only for missing details that affect implementation.

Ask one question at a time during startup. Do not send a multi-question checklist as the first response.

Startup order:

1. Ask target platform and confirm Web frontend.
2. Ask reference type: URL, mockup, Figma design, screenshot, or PRD.
3. If the reference type is URL:
   - If the user wants full website cloning, switch to Website Clone Mode and skip stack selection.
   - Otherwise, use React only for URL-based generation/restoration.
4. If the reference type is screenshot, mockup, Figma design, static design export, or UI image, switch to Screenshot Design Mode and ask React or Vue.
5. If the reference type is PRD, switch to PRD OpenDesign Mode and skip stack selection.
6. Ask for reference materials only if none were already provided.
7. Ask the single highest-impact missing question after analysis.

Do not default to Vite + React, Next.js, Vue, or any other stack before asking. Recommend a default only after the user asks for advice or says they have no preference.

Exception: in Website Clone Mode, the stack is fixed by `JCodesMore/ai-website-cloner-template`: Next.js + React + TypeScript + Tailwind + shadcn/ui.

Exception: in Screenshot Design Mode, the generation stack must be React + Tailwind or Vue + Tailwind, and the user must choose React or Vue.

Exception: URL-based generation/restoration outside Website Clone Mode supports React only.

Exception: in PRD OpenDesign Mode, use `JCodesMore/ai-website-cloner-template` with Next.js + React + TypeScript + Tailwind + shadcn/ui, and use Open Design as the design-stage source.

## Website Clone Mode

Trigger this mode when the user asks to fully clone/copy/reproduce a URL as a complete website, including all observable routes/pages and interactions.

Do not treat this as a normal high-fidelity frontend task. Use `JCodesMore/ai-website-cloner-template` as the required foundation and follow its `/clone-website <target-url...>` or Codex-compatible clone-website workflow when available.

Confirm only the essentials, one at a time:

- Which URL(s) should be cloned, if not already clear.
- Whether the user owns/has permission to clone the site, if there is risk of impersonation or protected content.
- Whether the goal is exact cloning or style imitation. If style imitation, do not use this mode; use Open Design/style-reference workflow.

Website Clone Mode must cover:

- Full Page Reconnaissance before implementation; do not rely on the first viewport only.
- All observable pages/routes.
- Navigation and link behavior.
- Hover, active, focus, selected, disabled states.
- Click effects, modals, drawers, menus, tabs, accordions, carousels, filters, forms, pagination.
- Carousel/gallery/slider behavior: controls, drag/swipe, scroll snap, pagination, active states, hover/click/focus, autoplay/pause, loop/clamp, responsive variants.
- Scroll behavior, sticky/fixed areas, horizontal overflow, responsive breakpoints.
- Visual tokens, assets, media, typography, spacing, colors, radii, shadows, motion.
- Proprietary media handling: do not directly reuse protected images, logos, brand assets, paid media, or distinctive artwork. Ask the user to choose one strategy: user-provided usable assets, user-authorized asset library, image2/image-generation replacement imagery, or same-size solid-color/gradient/skeleton placeholder blocks. Preserve geometry and hover/click/motion behavior for all strategies.
- Interaction/motion inventory with page/route, region, trigger, initial state, changed state, motion, scroll threshold, responsive difference, implementation status, and notes.
- Visual QA and README run instructions.

## Screenshot Design Mode

Trigger this mode when the user provides a screenshot, mockup, Figma design, UI image, or static design export as the primary reference.

Use `abi/screenshot-to-code` as the required generation workflow when available. It supports converting screenshots, mockups, and Figma designs into clean code, including React + Tailwind and Vue + Tailwind.

Ask one question before generation:

```text
Do you want the generated project to use React or Vue?
```

Then:

- Use React + Tailwind or Vue + Tailwind according to the user's answer.
- Treat screenshot-to-code output as the initial implementation, not final acceptance.
- Continue with layout, scroll, interaction, responsive, README, mock/API, and visual verification rules.
- Ask for interaction notes when static references do not reveal hover/click/active states.

## PRD OpenDesign Mode

Trigger this mode when the primary reference is a PRD.

Use `JCodesMore/ai-website-cloner-template` as the required frontend project foundation. Do not ask the user to choose the stack; use Next.js + React + TypeScript + Tailwind + shadcn/ui.

Use Open Design as the design-stage source. Prefer MCP-first integration:

- Keep `nexu-io/open-design` and `stackblitz-labs/bolt.diy` as separate projects.
- Connect them through Open Design MCP and bolt.diy MCP settings.
- Do not hard-merge Open Design source into bolt.diy for the first version.

Use Open Design material in this order:

1. `DESIGN.md` for design rules.
2. `tokens.css` for variables/tokens.
3. `components.html` or component references for component shape and layout.
4. Artifacts/prototypes/entry HTML for page structure and visual reference.

When bolt.diy is used, require the generation prompt or system prompt to:

- Read the active Open Design project through MCP.
- Use `DESIGN.md` as the primary visual authority.
- Use `tokens.css` as CSS variable source.
- Use component/prototype references when available.
- Generate React frontend code according to the PRD.
- Generate `docs/prd-coverage.md` mapping PRD requirements to routes/files/components.
- Run/preview/build in WebContainer and repair issues.

## 1. Platform and Stack

- Target: Web frontend.
- Stack: existing repo stack, React, Vue, Next.js, or Vite.
- Constraints: package manager, UI library, browser support, mobile support, deployment target.

## 2. References

Accept URLs, screenshots, design files, PRDs, sketches, competitor pages, and existing repositories.

If a design link cannot be accessed, ask for exported screenshots and any interaction notes.

When a URL is provided, inspect it as an interactive reference when tools are available:

- Visual tokens: color, typography, spacing, radius, shadow, density, background, breakpoints.
- Layout: viewport, below-fold content, sticky/fixed elements, scroll containers, responsive changes.
- Interactions: hover, active, focus, selected, disabled, click, modal, drawer, dropdown, tab, carousel, filter, sort, pagination, forms.
- Motion: transitions, easing, hover movement, open/close behavior, section reveal, media behavior, scroll-triggered UI changes.
- Complex components: carousel, gallery, slider, film strip, product selector, media viewer, horizontal rail, tabbed content. Inspect controls, pagination, active/disabled states, drag/swipe, scroll snap, autoplay/pause, keyboard/focus, item sizing, peeking cards, and responsive behavior.
- Content treatment: images, icons, badges, truncation, empty states.

Before implementation, create an interaction/motion inventory. Cover top, mid-scroll, bottom, key sections, large-screen/mobile widths, and triggers such as hover, click, focus, scroll, resize, drag, load, submit, and media events. Include scroll-driven UI states such as header/nav transformations, sticky capsule bars, CTA reveal/hide, parallax, element scale/fade, lazy loading, and bottom-state changes.

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
- Large-screen, tablet, and mobile viewports to verify.

## 8. Confirmation Gate

Before coding, summarize:

- Pages and route map.
- Business flows.
- Click event map.
- Scroll map.
- Layout confirmation HTML plan.
- Open questions.

Proceed only after user confirmation or explicit permission to decide.
