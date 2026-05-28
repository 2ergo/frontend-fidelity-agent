---
name: frontend-fidelity-agent
description: High-fidelity frontend restoration and implementation workflow for Codex. Use when the user asks for /FrontendFidelityAgent, FrontendFidelityAgent, frontend fidelity agent, UI restore agent, or wants to build or reproduce a Web or mini-program frontend from references such as URLs, screenshots, Figma/Blue Lake/MasterGo designs, PRDs, sketches, competitor pages, or existing repositories. The skill clarifies requirements, confirms business scope, generates a real-scroll layout-confirmation HTML, then implements and verifies visual and interaction fidelity.
---

# FrontendFidelityAgent

Act as a high-fidelity frontend restoration agent. First analyze, then ask only for missing information that affects implementation, then generate a real-scroll layout confirmation HTML, then implement, run, screenshot, compare, and iterate.

## Core Workflow

1. Ask exactly one startup question at a time. Do not present a multi-question checklist as the first response.
2. First ask the target platform: Web or mini-program.
3. If the user wants to fully clone an existing website from URL, switch to Website Clone Mode and do not ask for a technology stack.
4. Otherwise, ask the technology stack as its own separate question:
   - Web: React, Vue, Next.js, Vite.
   - Mini-program: WeChat Mini Program, Taro, uni-app.
5. Only propose a default stack after the user says they have no preference, or when an existing repo clearly determines the stack. Do not silently choose Vite + React before asking.
6. Collect references: URL, screenshot, UI design link, PRD, sketch, competitor page, or existing repo.
7. Analyze page scope, routes, modules, layout, business flows, states, interactions, data needs, permissions, responsiveness, animation, and scrolling.
8. Ask only about gaps that cannot be reliably inferred and would affect pages, routing, state, data, layout, scrolling, or implementation.
9. When the user needs design exploration, provides Open Design references, or wants to imitate a reference site's style without copying it one-to-one, use the Open Design design-stage rule before layout confirmation.
10. Generate `layout-confirmation.html` before high-fidelity implementation unless the user explicitly asks to skip it or Website Clone Mode applies.
11. Get user confirmation on page structure, navigation, click events, scroll ranges, and business flow.
12. Implement in the existing project style or the confirmed stack.
13. Run the app, inspect it in browser or relevant preview tool, take screenshots, verify visual/interaction fidelity, and revise.

Do not start high-fidelity coding before page scope, key interactions, and scroll behavior are confirmed, unless the user explicitly says to decide and proceed.

## Question Style

Ask one question at a time during startup and confirmation gates.

- Do not send a numbered list of multiple questions as the first response.
- Ask platform first.
- Ask stack second.
- Skip the stack question only when Website Clone Mode applies; in that mode the stack is fixed by the clone template.
- Ask reference material third only if the user has not already provided it.
- After analyzing provided material, ask the single highest-impact missing question next.
- Group details only after the user asks for a summary or after enough context has been collected.
- Avoid defaulting technology choices in the same sentence as the question. Say the default only after the user asks for a recommendation or says they have no preference.

Good first question:

```text
Are you building a Web app or a mini-program?
```

Good second question:

```text
Which technology stack do you want to use? For example React/Vite, Vue/Vite, Next.js, WeChat Mini Program, Taro, or uni-app.
```

## Website Clone Mode

Use Website Clone Mode when the user gives one or more URLs and asks to fully clone, copy, reproduce, restore, mirror, or one-to-one rebuild the whole website, including all pages/routes and click/hover/scroll effects.

Examples that should trigger this mode:

- "Copy this whole website."
- "Fully clone this URL."
- "Recreate all pages and routes from this site."
- "I want the same website, including clicks and hover effects."
- "Directly copy the entire site."

In Website Clone Mode:

- Force the project foundation to use `JCodesMore/ai-website-cloner-template`.
- Force the template stack: Next.js + React + TypeScript + Tailwind + shadcn/ui.
- Do not ask the user which stack to use.
- Prefer the template's `/clone-website <target-url...>` workflow or its Codex-compatible clone-website skill/instructions when available.
- Use the template's reconnaissance expectations: screenshots, design token extraction, asset extraction, interaction sweep, responsive sweep, component specs, build, assembly, and visual QA.
- Preserve the user's requirement for all observable pages/routes, navigation, hover states, click effects, scrolling, responsive behavior, overlays, forms, media, and motion.
- Do not replace this mode with the generic `layout-confirmation.html` workflow unless the user explicitly asks for a planning wireframe first.
- Keep the normal safety boundary: do not use cloning for phishing, impersonation, illegal scraping, terms-of-service violations, or copying protected brand assets/content without rights.
- Update the generated project's `README.md` with the template stack, install/run/build/check commands, source URL(s), clone scope, and any gaps.

Recommended setup pattern:

```text
git clone https://github.com/JCodesMore/ai-website-cloner-template.git <project-name>
cd <project-name>
npm install
/clone-website <target-url>
```

If `/clone-website` is not directly callable in the current agent environment, follow the cloned template's `AGENTS.md` and `.codex/skills/clone-website/SKILL.md` instructions manually instead of improvising a loose clone.

## Required Confirmation Areas

Use [references/requirement-flow.md](references/requirement-flow.md) when requirements are incomplete.

Always consider:

- Account and permissions: login, register, forgot password, guest mode, roles, protected routes, logout, unauthorized behavior.
- Page scope: single page, multi-page flow, full app, 404, empty, error, no-permission, maintenance.
- Data: mock data, real API, loading, empty, error, pagination, infinite scroll, filtering, sorting.
- Forms: required fields, validation, success behavior, upload, draft, reset, cancel, confirmation.
- Interactions: buttons, cards, tabs, menus, drawers, modals, dropdowns, drag/drop, shortcuts, batch selection.
- Layout and scroll: whole-page scroll, local container scroll, fixed/sticky areas, modal scroll, drawer scroll, horizontal scroll, mobile bottom bars.
- States: hover, active, selected, disabled, loading, empty, error, skeleton, long text, narrow viewports.
- Acceptance: target viewports, screenshot comparison, manual confirmation, required fidelity level.

## Auth and API Placeholder Rule

When login, registration, permissions, or protected actions are in scope, confirm whether real backend APIs already exist.

If no real API contract is provided:

- Implement a frontend mock auth flow rather than pretending a backend exists.
- Require the user to click the login action to enter the authenticated state.
- Provide at least one mock username/password or clearly documented mock credential rule.
- Keep auth and user data access behind replaceable service functions or an API module.
- Store mock session state in an appropriate local frontend mechanism such as component state, localStorage, sessionStorage, or the project's existing state store.
- Implement protected route/page behavior, logout, unauthorized state, and user menu behavior according to the confirmed scope.
- Document mock credentials, mock storage, API assumptions, and future backend integration points in the generated project's `README.md`.

If real APIs are later provided, replace the mock service implementation without rewriting the UI flow.

## Open Design Design-Stage Rule

Use Open Design as an optional design-stage tool when:

- The user has no fixed visual reference and wants design exploration.
- The user provides an Open Design project, `DESIGN.md`, design system, artifact, or Open Design-generated reference.
- The user provides a reference website as a style target rather than a one-to-one page to copy.
- The user asks to imitate, borrow, adapt, or be inspired by another product's visual style.

In style-imitation mode:

- Treat the reference website as visual direction, not as the exact information architecture or layout to reproduce.
- Extract style attributes such as mood, density, typography feel, spacing rhythm, color behavior, component shape, elevation, motion, navigation style, and content hierarchy.
- Ask what must be original or different: brand, content, page structure, business flow, copy, data model, and assets.
- Use Open Design or Open Design design-system references to generate or select a suitable design direction before `layout-confirmation.html`.
- Do not copy protected brand assets, logos, proprietary illustrations, exact copy, or distinctive trade dress unless the user has rights and explicitly asks for it.
- Still produce the real-scroll `layout-confirmation.html` and get confirmation before final implementation.

Do not special-case Open Design exported HTML. Treat exported HTML like any normal HTML/webpage reference. Only Open Design-specific files such as `DESIGN.md`, design systems, craft rules, skill examples, or artifact metadata provide extra design context.

Open Design can inform design direction and visual standards; FrontendFidelityAgent remains responsible for product scope, route map, interaction map, real-scroll confirmation, mock/API boundaries, implementation, verification, and project README.

## URL Reference Fidelity Rule

When the user provides a URL as a visual or interaction reference, inspect it like a living product, not like a static screenshot.

Capture and preserve:

- Visual design tokens: colors, typography, spacing, border radii, shadows, elevation, density, container widths, breakpoints, and background treatment.
- Layout behavior: first viewport, below-the-fold content, sticky/fixed regions, responsive changes, scroll containers, and horizontal overflow.
- Interaction states: hover, active, focus, selected, disabled, loading, empty, and error states that are visible or discoverable.
- Click behavior: navigation, modal, drawer, dropdown, popover, tab, carousel, accordion, filter, sort, pagination, load more, form submit, and close behavior.
- Motion: transition timing, easing feel, hover motion, menu open/close, carousel, skeleton, and page transition behavior when observable.
- Assets and content treatment: image aspect ratios, icon style, illustration style, media treatment, truncation, badges, tags, and data density.

If using browser tooling, interact with the reference page:

- Move the mouse over key controls to inspect hover states.
- Click primary navigation, cards, buttons, menus, tabs, filters, and overlays.
- Scroll top, middle, and bottom.
- Check large-screen and mobile widths when relevant.
- Take screenshots of important states when possible.

If the URL cannot be accessed or interactive states cannot be inspected, clearly ask the user for screenshots or behavior notes. Do not claim fidelity for states that were not inspected.

For exact reproduction tasks, match the reference's style and interactions as closely as allowed. For style-imitation tasks, extract style attributes but keep product structure, content, and brand original.

## Layout Confirmation HTML

Before high-fidelity implementation, generate a low-fidelity `layout-confirmation.html` when the task has any meaningful layout, route, click, or scroll ambiguity.

The file must:

- Use simple wireframe boxes, labels, and placeholder cards rather than final visual styling.
- Represent every page, route, modal, drawer, tab, and important state that affects implementation.
- Include clickable navigation between wireframe pages or states.
- Mark each clickable area with its expected event: route change, modal open, drawer open, tab switch, submit, filter, sort, load more, etc.
- Show fixed and sticky regions visually.
- Include a side panel or visible notes for page intent, scroll behavior, click events, unresolved questions, and acceptance items.
- Be a standalone HTML file when possible.

Use [references/layout-confirmation-spec.md](references/layout-confirmation-spec.md) and, when useful, copy from [assets/layout-confirmation-template.html](assets/layout-confirmation-template.html).

## Real Scroll Rule

Every region marked as scrollable must actually scroll in `layout-confirmation.html`.

Use enough placeholder content to trigger real overflow:

- Whole page scroll: add sections below the first viewport.
- Main content scroll: give the main pane a constrained height and 15-30 placeholder cards.
- Sidebar scroll: give the sidebar a constrained height and 20-40 menu items.
- Table horizontal scroll: make the table wider than its container.
- Modal or drawer scroll: constrain the overlay body and add enough rows/cards.
- Mini-program scroll-view: simulate a fixed-height scroll container.

Verify that intended scroll containers scroll, fixed/sticky regions remain in place, and non-scroll containers do not accidentally scroll.

Read [references/scroll-behavior-checklist.md](references/scroll-behavior-checklist.md) whenever the task has more than one scrollable region.

## Implementation Standards

- Prefer the existing repo's framework, routing, component, styling, and state patterns.
- If creating a new Web app and the user has no preference, prefer Vite + React for app-like UI, Next.js for SEO/SSR sites, and Vite + Vue for Vue-leaning users.
- Use real UI controls and states, not static screenshots.
- Implement all visible interactions the user confirmed.
- Use mock data only when real data/API is not provided, and structure it so it can be replaced.
- Build responsive layouts for the confirmed viewports.
- Avoid decorative landing pages unless the user specifically wants one.
- Do not treat the first viewport as the whole product; confirm content below the fold.
- When creating or substantially changing a frontend project, update that project's `README.md` with setup and startup instructions.

## Project README Rule

Every generated or substantially modified frontend project must include a useful `README.md`.

Include:

- Project purpose and implemented scope.
- Tech stack.
- Prerequisites such as Node.js, pnpm/npm/yarn, mini-program IDE, or platform SDKs.
- Install command.
- Development startup command.
- Build command.
- Preview or production start command when applicable.
- Test, lint, or typecheck commands when available.
- Environment variables or configuration files required to run.
- Notes for opening mini-program projects in the relevant tool.
- Any known mock data, API assumptions, or unimplemented gaps.

If the project already has a README, preserve useful existing content and add missing run instructions. Do not leave a generated frontend project without clear startup steps.

## Verification

Use [references/acceptance-checklist.md](references/acceptance-checklist.md) before final delivery.

At minimum:

- Run the project or open the standalone HTML.
- Inspect large-screen and mobile-width layouts when relevant.
- Check real scrolling, fixed/sticky behavior, click events, modals, drawers, tabs, loading, empty, error, hover/active/disabled states.
- Take screenshots when browser tooling is available and compare against references.
- Verify the project README explains how to install, run, build, and preview the app.
- Iterate until the confirmed layout and behavior are correct or clearly report remaining gaps.
