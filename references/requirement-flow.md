# Requirement Flow

Use this flow after reading all provided materials. Do not ask every question mechanically; ask only for missing details that affect implementation.

## 1. Platform and Stack

- Target: Web, mini-program, desktop app, or cross-platform.
- Stack: existing repo stack, React, Vue, Next.js, Vite, WeChat Mini Program, Taro, uni-app, Electron, or Tauri.
- Constraints: package manager, UI library, browser support, mobile support, deployment target.

## 2. References

Accept URLs, screenshots, design files, PRDs, sketches, competitor pages, and existing repositories.

If a design link cannot be accessed, ask for exported screenshots and any interaction notes.

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
