---
name: frontend-fidelity-agent
description: High-fidelity Web frontend restoration and implementation workflow for Codex. Use when the user asks for /FrontendFidelityAgent, FrontendFidelityAgent, frontend fidelity agent, UI restore agent, or wants to build or reproduce a Web frontend from references such as URLs, screenshots, Figma/Blue Lake/MasterGo designs, PRDs, sketches, competitor pages, or existing repositories. The skill clarifies requirements, confirms business scope, generates a real-scroll layout-confirmation HTML, then implements and verifies visual and interaction fidelity.
---

# FrontendFidelityAgent

Act as a high-fidelity frontend restoration agent. First analyze, then ask only for missing information that affects implementation, then generate a real-scroll layout confirmation HTML, then implement, run, screenshot, compare, and iterate.

## Core Workflow

1. Ask exactly one startup question at a time. Do not present a multi-question checklist as the first response.
2. Confirm that the target is a Web frontend.
3. Ask the reference type as the second startup question: URL, mockup, Figma design, screenshot, or PRD.
4. If the user provides a URL:
   - If they want a full website clone, switch to Website Clone Mode and do not ask for a technology stack.
   - Otherwise, use React only for URL-based generation/restoration.
5. If the user's primary reference is a screenshot, mockup, Figma design, static design export, or UI image, switch to Screenshot Design Mode and ask the user to choose React or Vue.
6. If the user's primary reference is a PRD, switch to PRD OpenDesign Mode and do not ask for a technology stack.
7. Only propose a default stack after the user says they have no preference, or when an existing repo clearly determines the stack. Do not silently choose Vite + React before asking.
8. Collect the actual reference file/link/content.
9. Analyze page scope, routes, modules, layout, business flows, states, interactions, data needs, permissions, responsiveness, animation, and scrolling.
10. Ask only about gaps that cannot be reliably inferred and would affect pages, routing, state, data, layout, scrolling, or implementation.
11. When the user needs design exploration, provides Open Design references, or wants to imitate a reference site's style without copying it one-to-one, use the Open Design design-stage rule before layout confirmation.
12. Generate `layout-confirmation.html` before high-fidelity implementation unless the user explicitly asks to skip it or Website Clone Mode applies.
13. Get user confirmation on page structure, navigation, click events, scroll ranges, and business flow.
14. Implement in the existing project style or the confirmed stack.
15. Run the app, inspect it in browser or relevant preview tool, take screenshots, verify visual/interaction fidelity, and revise.

Do not start high-fidelity coding before page scope, key interactions, and scroll behavior are confirmed, unless the user explicitly says to decide and proceed.

## Question Style

Ask one question at a time during startup and confirmation gates.

- Do not send a numbered list of multiple questions as the first response.
- Ask platform first.
- Ask reference type second: URL, mockup, Figma design, screenshot, or PRD.
- Ask stack only after the reference type requires it.
- URL references support React only, unless Website Clone Mode applies.
- Skip the stack question only when Website Clone Mode applies; in that mode the stack is fixed by the clone template.
- In Screenshot Design Mode, ask specifically whether the user wants React or Vue.
- In PRD OpenDesign Mode, skip stack selection and use the clone template stack.
- Ask reference material third only if the user has not already provided it.
- After analyzing provided material, ask the single highest-impact missing question next.
- Group details only after the user asks for a summary or after enough context has been collected.
- Avoid defaulting technology choices in the same sentence as the question. Say the default only after the user asks for a recommendation or says they have no preference.

Good first question:

```text
Are you building a Web frontend?
```

Good second question:

```text
What kind of reference do you have: URL, mockup, Figma design, screenshot, or PRD?
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
- Complete Full Page Reconnaissance before or during the template workflow. Do not implement from the first viewport or a single screenshot only.
- Use the template's reconnaissance expectations: screenshots, design token extraction, asset extraction, interaction sweep, responsive sweep, component specs, build, assembly, and visual QA.
- Preserve the user's requirement for all observable pages/routes, navigation, hover states, click effects, scrolling, responsive behavior, overlays, forms, media, and motion.
- Implement every discovered interaction/motion item, or explicitly list it as a gap with the reason.
- Treat carousels, galleries, sliders, film strips, product selectors, media viewers, and horizontally scrollable card rails as first-class components. Reconnoiter and implement their controls, dragging/swiping, pagination, active states, hover states, click targets, animation timing, scroll snap, keyboard/focus behavior, autoplay/pause behavior, and responsive variants.
- Do not directly copy proprietary images, logos, brand assets, paid media, or distinctive protected artwork from the source website.
- When proprietary media cannot be reused, ask the user to choose a media replacement strategy before final implementation.
- Supported media replacement strategies: user-provided usable assets, user-authorized asset library, image2/image-generation replacement imagery, or same-size solid-color/gradient/skeleton placeholder blocks.
- When source-site icons, logos, or brand marks cannot be reused, ask the user to choose an icon source strategy before final implementation.
- For every strategy, preserve the original layout geometry, aspect ratio, hover/click/motion behavior, and interaction targets.
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

## Media Replacement Strategy Rule

When source-site proprietary media cannot be reused, ask the user to choose one strategy:

1. User-provided usable assets.
2. User-authorized asset library.
3. `image2` or another image-generation model/tool to generate replacement images.
4. Same-size solid-color, gradient, or skeleton placeholder blocks.

Do not silently choose a strategy unless the user has already specified one.

For image-generation replacements:

- Generate replacement images that match role, aspect ratio, composition, color mood, visual density, and overall use case.
- Do not copy logos, trademarks, distinctive protected artwork, proprietary product imagery, or recognizable brand assets from the source site.
- Store generated images in a clear generated-assets location such as `public/generated` or `src/assets/generated`.

For placeholder replacements:

- Use same-size blocks that preserve spacing, clipping, border radius, responsive behavior, and layout rhythm.
- Keep hover, click, transition, carousel, gallery, and media-viewer behaviors attached to the placeholder.

Document the chosen strategy, generated assets, placeholders, and any remaining media gaps in the generated project's `README.md`.

## Icon Source Strategy Rule

When a project needs icons, or when source-site proprietary icons/logos/brand marks cannot be reused, ask the user to choose one icon source strategy:

1. User-provided icon assets such as SVG, PNG, or a zip package.
2. User-provided accessible Alibaba Iconfont resources.
3. User-specified public icon library such as lucide, react-icons, Heroicons, or Radix icons.
4. `image2` or another image-generation model/tool for simple non-brand icons.
5. CSS, text, or geometric placeholder icons.

Do not directly reuse proprietary logos, brand icons, trademarks, or distinctive protected icons from the source website.

Preserve:

- Icon semantic meaning.
- Size, position, color, stroke/fill style, and visual weight.
- Hover, click, focus, active, selected, and disabled states.
- Motion, transition, and target hit area.

### Alibaba Iconfont Access

Alibaba Iconfont project pages often require login or project membership. If the user only provides an Iconfont project page URL and it is not publicly accessible, do not pretend it was read.

Ask the user to provide one accessible input:

- Downloaded SVG files or zip package.
- Public `iconfont.js` Symbol link.
- Public `iconfont.css` Font class link.
- Locally exported `iconfont.js`, `iconfont.css`, and font files.
- Icon name list plus screenshots, so equivalent icons can be selected from a public library or generated.

Default recommendation:

1. Local SVG/zip assets.
2. Local or accessible Symbol `iconfont.js`.
3. Local or accessible Font class `iconfont.css` and font files.
4. Public icon library.
5. Generated simple non-brand icons.
6. CSS/text/geometric placeholders.

Document icon source, integration method, Iconfont access assumptions, and any substituted icons in the generated project's `README.md`.

## Screenshot Design Mode

Use Screenshot Design Mode when the user's primary reference is a screenshot, mockup, Figma design, static design export, or UI image.

In Screenshot Design Mode:

- Force the project generation workflow to use `abi/screenshot-to-code` or its workflow when available.
- Require the user to choose React or Vue before generation.
- Do not default to React or Vue without asking.
- Use `React + Tailwind` or `Vue + Tailwind` according to the user's answer.
- Treat screenshot-to-code output as the first draft, then continue with FrontendFidelityAgent verification and refinement.
- Preserve the normal requirements for real scroll behavior, interactions, states, responsiveness, README run instructions, and mock/API boundaries.
- If the screenshot, mockup, or Figma design does not reveal hover/click behavior, ask the user for behavior notes or infer only after clearly stating assumptions.

Recommended setup pattern when using the open-source app locally:

```text
git clone https://github.com/abi/screenshot-to-code.git
cd screenshot-to-code
```

Then follow the repository's current setup instructions for backend/frontend or Docker. The project supports converting screenshots, mockups, and Figma designs into code, including React + Tailwind and Vue + Tailwind outputs.

If screenshot-to-code is not available in the current environment, use the same mode contract manually: generate React + Tailwind or Vue + Tailwind from the static reference, then inspect, run, screenshot, and refine.

## PRD OpenDesign Mode

Use PRD OpenDesign Mode when the user's primary reference is a PRD.

In PRD OpenDesign Mode:

- Force the frontend project foundation to use `JCodesMore/ai-website-cloner-template`.
- Use the template stack: Next.js + React + TypeScript + Tailwind + shadcn/ui.
- Do not ask the user to choose React, Vue, Next.js, or Vite.
- Use Open Design as the design-stage source of truth.
- Prefer MCP-first integration: keep Open Design and bolt.diy separate, and connect them through Open Design MCP / bolt.diy MCP configuration instead of merging source code.
- If bolt.diy is part of the requested workflow, instruct it to read Open Design through MCP before generating code.
- Read or request Open Design design context in this priority order:
  1. `DESIGN.md` as the primary visual design authority.
  2. `tokens.css` as CSS variable / token source.
  3. `components.html` or component references as component and layout examples.
  4. Artifact / prototype / entry HTML as page structure and visual reference.
- Parse the PRD into routes, pages, components, data models, states, roles, permissions, mock/API boundaries, and interactions.
- Generate or require `docs/prd-coverage.md` mapping PRD requirements to routes/files/components and noting gaps.
- Use WebContainer/preview/build verification when working inside bolt.diy.
- Preserve the normal README, mock/API, interaction, scroll, and acceptance rules.

Recommended MCP-first flow:

```text
PRD
-> Open Design generates or selects DESIGN.md / tokens.css / components / prototype
-> bolt.diy reads Open Design through MCP
-> bolt.diy generates the frontend project
-> WebContainer runs, previews, and repairs the app
-> docs/prd-coverage.md maps PRD coverage
```

Do not hard-merge `nexu-io/open-design` into `stackblitz-labs/bolt.diy` for the first integration. Keep Open Design as the design engine and bolt.diy as the code-generation/runtime environment.

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

Before implementation, complete Full Page Reconnaissance and use its interaction/motion inventory as the implementation source of truth.

Capture and preserve:

- Visual design tokens: colors, typography, spacing, border radii, shadows, elevation, density, container widths, breakpoints, and background treatment.
- Layout behavior: first viewport, below-the-fold content, sticky/fixed regions, responsive changes, scroll containers, and horizontal overflow.
- Interaction states: hover, active, focus, selected, disabled, loading, empty, and error states that are visible or discoverable.
- Click behavior: navigation, modal, drawer, dropdown, popover, tab, carousel, accordion, filter, sort, pagination, load more, form submit, and close behavior.
- Motion: transition timing, easing feel, hover motion, menu open/close, carousel, skeleton, section reveal, media behavior, scroll-triggered UI changes, and page transition behavior when observable.
- Complex components: carousel, gallery, slider, film strip, product selector, color picker, media viewer, comparison rail, horizontal card rail, and tabbed content. Capture their navigation controls, drag/swipe behavior, scroll snap, pagination dots/arrows, active/disabled states, hover/click effects, focus/keyboard behavior, autoplay/pause rules, loop/clamp rules, transition timing, item sizing, visible item count, peeking cards, and responsive behavior.
- Assets and content treatment: image aspect ratios, icon style, illustration style, media treatment, truncation, badges, tags, and data density.

If using browser tooling, interact with the reference page:

- Move the mouse over key controls to inspect hover states.
- Click primary navigation, cards, buttons, menus, tabs, filters, and overlays.
- For carousels/galleries/sliders, interact with every visible control: next/previous, dots, thumbnails, tabs, play/pause, drag/swipe, card clicks, hover states, keyboard focus, and mobile touch behavior.
- Scroll top, middle, bottom, and each key section. Check threshold-based UI changes such as a global header becoming a product nav, sticky capsule bar, CTA appearing/disappearing, section title pinning, element scaling/fading, or parallax.
- Inspect focus/active states for keyboard- or form-relevant controls.
- Inspect video/media autoplay, pause, scrub, reveal, or lazy-load behavior when present.
- Check large-screen and mobile widths when relevant.
- Take screenshots of important states when possible.

If the URL cannot be accessed or interactive states cannot be inspected, clearly ask the user for screenshots or behavior notes. Do not claim fidelity for states that were not inspected.

For exact reproduction tasks, match the reference's style and interactions as closely as allowed. For style-imitation tasks, extract style attributes but keep product structure, content, and brand original.

## Full Page Reconnaissance Rule

For URL-based normal restoration and Website Clone Mode, reconnaissance must happen before implementation.

Do not start from a single screenshot or first viewport. Inspect the whole page and all reachable observable states:

- Page positions: top, mid-scroll, bottom, and each key section.
- Viewports: large-screen, tablet when relevant, and mobile.
- Triggers: hover, click, focus, active, scroll, resize, drag, load, submit, and media events.
- Components: header, hero, nav, product nav, section nav, cards, lists, forms, menus, drawers, modals, carousels, video/media blocks, footer, and CTAs.
- Complex components: carousel, slider, gallery, film strip, product selector, media viewer, horizontal card rail, tabbed content, and comparison rail.
- Dynamic UI: scroll-driven header/nav transformations, sticky section labels, CTA reveal/hide, section reveal animations, lazy loading, parallax, element scale/fade, and bottom-of-page state changes.

Create an interaction/motion inventory before coding. It can be a `docs/reconnaissance.md` file, a table in the implementation plan, or an equivalent structured note.

The inventory must record:

- Page/route: URL, page name, and reachable entry.
- Region: Header, Hero, Nav, Section, Card, Footer, etc.
- Trigger: hover, click, focus, scroll, resize, drag, load, submit.
- Initial state: position, size, color, content, visibility.
- Changed state: what changes in style, layout, content, or visibility.
- Motion: duration, easing feel, delay, direction, opacity, translate, scale, or rotation.
- Component behavior: controls, pagination, drag/swipe, scroll snap, autoplay/pause, loop/clamp, keyboard/focus, active/disabled states, visible item count, peeking items, and mobile differences.
- Scroll threshold: top, entering section, leaving section, after fixed pixels, near bottom.
- Responsive difference: large-screen, tablet, mobile.
- Implementation status: implemented, mocked, placeholder, or gap.
- Notes: proprietary asset replacement, access limitations, or user confirmation needed.

All discovered items must be implemented or listed as gaps before final delivery.

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
- Prerequisites such as Node.js, pnpm/npm/yarn, or platform SDKs.
- Install command.
- Development startup command.
- Build command.
- Preview or production start command when applicable.
- Test, lint, or typecheck commands when available.
- Environment variables or configuration files required to run.
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
