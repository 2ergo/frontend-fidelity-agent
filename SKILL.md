---
name: frontend-fidelity-agent
description: High-fidelity frontend restoration and implementation workflow for Codex. Use when the user asks for /FrontendFidelityAgent, FrontendFidelityAgent, frontend fidelity agent, UI restore agent, or wants to build or reproduce a Web, mini-program, or desktop frontend from references such as URLs, screenshots, Figma/Blue Lake/MasterGo designs, PRDs, sketches, competitor pages, or existing repositories. The skill clarifies requirements, confirms business scope, generates a real-scroll layout-confirmation HTML, then implements and verifies visual and interaction fidelity.
---

# FrontendFidelityAgent

Act as a high-fidelity frontend restoration agent. First analyze, then ask only for missing information that affects implementation, then generate a real-scroll layout confirmation HTML, then implement, run, screenshot, compare, and iterate.

## Core Workflow

1. Identify target platform: Web, mini-program, or desktop app.
2. Select or confirm stack:
   - Web: React, Vue, Next.js, Vite.
   - Mini-program: WeChat Mini Program, Taro, uni-app.
   - Desktop: Electron, Tauri.
3. Collect references: URL, screenshot, UI design link, PRD, sketch, competitor page, or existing repo.
4. Analyze page scope, routes, modules, layout, business flows, states, interactions, data needs, permissions, responsiveness, animation, and scrolling.
5. Ask only about gaps that cannot be reliably inferred and would affect pages, routing, state, data, layout, scrolling, or implementation.
6. Generate `layout-confirmation.html` before high-fidelity implementation unless the user explicitly asks to skip it.
7. Get user confirmation on page structure, navigation, click events, scroll ranges, and business flow.
8. Implement in the existing project style or the confirmed stack.
9. Run the app, inspect it in browser or relevant preview tool, take screenshots, verify visual/interaction fidelity, and revise.

Do not start high-fidelity coding before page scope, key interactions, and scroll behavior are confirmed, unless the user explicitly says to decide and proceed.

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
- Desktop app panes: simulate fixed window height and independent panes.

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
- Prerequisites such as Node.js, pnpm/npm/yarn, mini-program IDE, Electron/Tauri requirements, or platform SDKs.
- Install command.
- Development startup command.
- Build command.
- Preview or production start command when applicable.
- Test, lint, or typecheck commands when available.
- Environment variables or configuration files required to run.
- Notes for opening mini-program or desktop app projects in the relevant tool.
- Any known mock data, API assumptions, or unimplemented gaps.

If the project already has a README, preserve useful existing content and add missing run instructions. Do not leave a generated frontend project without clear startup steps.

## Verification

Use [references/acceptance-checklist.md](references/acceptance-checklist.md) before final delivery.

At minimum:

- Run the project or open the standalone HTML.
- Inspect desktop and mobile-width layouts when relevant.
- Check real scrolling, fixed/sticky behavior, click events, modals, drawers, tabs, loading, empty, error, hover/active/disabled states.
- Take screenshots when browser tooling is available and compare against references.
- Verify the project README explains how to install, run, build, and preview the app.
- Iterate until the confirmed layout and behavior are correct or clearly report remaining gaps.
