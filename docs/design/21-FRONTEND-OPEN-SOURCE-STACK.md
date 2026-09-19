# MiLyfe Frontend Open-Source Stack

**Status:** Frontend architecture selection
**Brand name:** MiLyfe
**Naming rule:** The product is always written `MiLyfe`. No alternate spelling or substitute label is permitted.
**Design source:** Existing `milyfe.fun` and `miforge.milyfe.fun` are visual references only. They are being replaced and must not remain runtime dependencies.
**Theme:** MiLyfe light-theme design system
**Mode:** Design only; no code

## 1. Frontend decision

Use a single API-driven frontend monorepo built on:

- Next.js
- React
- TypeScript
- shadcn/ui
- Radix Primitives
- Tailwind CSS
- TanStack Query
- TanStack Table
- TanStack Form
- Zod
- Dexie.js core for local-first storage
- next-intl for localization
- MapLibre GL JS for maps
- Tiptap for owned rich-content editing where needed
- Lucide icons
- Storybook
- Vitest
- Playwright
- Testing Library and axe-core

The frontend does not become the backend. It consumes the backend contracts, displays authority and receipts, and submits commands through the API.

## 2. Selected repositories

### Application framework

- <https://github.com/vercel/next.js>

Next.js provides the public campaign site, authenticated MiLyfe application, server rendering where useful, routing, caching, and build tooling. The official repository also contains agent skills, which is useful for an AI-configurable codebase. Use standard self-hosted Node deployment rather than assuming Vercel hosting.

Decision: **Use Next.js App Router. Do not add TanStack Router.** One routing system is enough.

### React

- <https://github.com/facebook/react>

React is the UI foundation used by Next.js and the selected component ecosystem.

### Design system and accessible primitives

- <https://github.com/shadcn-ui/ui>
- <https://github.com/radix-ui/primitives>
- <https://github.com/tailwindlabs/tailwindcss>

`shadcn/ui` is a code-ownership model rather than a black-box runtime component dependency. MiLyfe will own the copied and branded components. Radix provides accessible interaction primitives. Tailwind supplies the token and layout utility layer.

Decision: **Use shadcn/ui + Radix + Tailwind as the MiLyfe component foundation.** Do not install several competing component libraries.

### Server state, tables, forms, and schemas

- <https://github.com/TanStack/query>
- <https://github.com/TanStack/table>
- <https://github.com/TanStack/form>
- <https://github.com/colinhacks/zod>

Use TanStack Query for API state, caching, invalidation, retries, and optimistic behavior only where the backend contract permits it. Use TanStack Table for receipts, ledgers, case files, campaign records, and operator tables. Use TanStack Form and Zod for typed forms and validation.

The frontend must not invent its own copy of backend rules. Zod schemas can validate user input, but authoritative validation remains in the backend.

### Offline and local-first

- <https://github.com/dexie/Dexie.js>
- <https://github.com/GoogleChrome/workbox>

Use Dexie.js core for IndexedDB-backed local data, drafts, offline queues, cached receipts, and pending commands. Use Workbox only where service-worker behavior requires it.

Decision: **Use Dexie.js core only. Do not depend on Dexie Cloud.** MiLyfe sync, conflict resolution, permissions, and receipts must remain controlled by the MiLyfe backend.

Offline behavior must distinguish:

- Local draft
- Queued command
- Locally verified action
- Server-accepted action
- Conflict
- Rejected action
- Reconciliation complete

### Localization

- <https://github.com/amannn/next-intl>
- <https://github.com/i18next/react-i18next>

Decision: **Use one localization system.** For the selected Next.js application, use `next-intl` unless backend or mobile requirements later justify a shared i18next layer.

Localization must support:

- English first
- Locale-aware dates, times, numbers, and money
- Plain-language mode
- Right-to-left readiness
- Localized routes where useful
- Community translation review
- Legal, health, justice, and campaign terminology review

### Maps and place interfaces

- <https://github.com/maplibre/maplibre-gl-js>

MapLibre is the map-rendering layer for Jacksonville/Duval place views, mobility, services, emergency resources, local ventures, and future cells. Map tiles and geocoding are separate infrastructure decisions; MapLibre itself does not provide free global map data or hosting.

### Knowledge and campaign editing

- <https://github.com/ueberdosis/tiptap>
- <https://github.com/ueberdosis/tiptap-ui-components>

Use Tiptap for owned rich-content editing in MiKnowledge, Campaign OS, MiMedia, MiForge venture descriptions, and public-office publishing where needed.

Every document needs source, author, version, permissions, publication status, correction history, and export behavior.

### Icons and restrained motion

- <https://github.com/lucide-icons/lucide>
- <https://github.com/motiondivision/motion>

Use Lucide for consistent icons. Use motion sparingly and respect reduced-motion settings. Motion must never be required to understand a receipt, approval, safety warning, or money state.

### Component development and testing

- <https://github.com/storybookjs/storybook>
- <https://github.com/microsoft/playwright>
- <https://github.com/vitest-dev/vitest>
- <https://github.com/testing-library/react-testing-library>
- <https://github.com/dequelabs/axe-core>

Storybook is the source of truth for component states and interaction documentation. Playwright covers browser, journey, offline, permission, and visual checks. Vitest covers fast unit and contract tests. Testing Library tests user-facing behavior. axe-core runs automated accessibility checks, followed by manual keyboard and screen-reader review.

## 3. Frontend repository structure

The frontend monorepo should be organized around product surfaces and shared contracts:

- `apps/milyfe-web` — authenticated MiLyfe application
- `apps/mijaxx-web` — public campaign and mayor-campaign interface
- `apps/miforge-web` — builder and venture interface
- `apps/storybook` — component and pattern workshop
- `packages/ui` — owned MiLyfe components
- `packages/brand` — MiLyfe tokens, typography, icons, assets, themes
- `packages/api-client` — generated backend client
- `packages/contracts` — shared OpenAPI, JSON Schema, event, receipt, and status types
- `packages/auth` — session and context adapters
- `packages/offline` — Dexie stores, queue, sync state, and conflict UI
- `packages/i18n` — translation keys and locale rules
- `packages/maps` — MapLibre wrappers and place layers
- `packages/editor` — Tiptap configurations
- `packages/testing` — test fixtures and accessibility helpers
- `packages/analytics` — privacy-preserving event definitions
- `docs/ui` — interaction decisions and content guidelines

The public campaign site, MiForge site, and authenticated MiLyfe app share the same brand package but have different data permissions and publishing boundaries.

## 4. UI source-of-truth rules

- Backend OpenAPI and JSON Schema define data shape.
- Backend permissions define access.
- Backend receipts define completed actions.
- Backend MiMoney defines balances and settlement.
- Frontend design tokens define visual appearance.
- Storybook defines component states.
- Accessibility tests define minimum interaction behavior.
- No UI-only state may imply a financial, legal, health, election, or governance outcome that the backend has not accepted.

## 5. Light-theme MiLyfe design system

The new system uses owned design tokens derived from the visual direction of the existing MiLyfe websites. The old sites are not imported.

Required token groups:

- Background
- Surface
- Elevated surface
- Primary text
- Secondary text
- Muted text
- Border
- Brand accent
- Positive
- Caution
- Critical
- Information
- Focus
- Disabled
- Typography
- Spacing
- Radius
- Shadow
- Motion
- Breakpoints

The final color values, typography, logo assets, and imagery must be approved as MiLyfe-owned assets before implementation. Do not guess or hardcode a new brand palette from memory.

## 6. AI-agent configuration

The frontend repository must include:

- Root `AGENTS.md`
- `apps/*/AGENTS.md`
- `.agents/skills/frontend-architecture`
- `.agents/skills/design-system`
- `.agents/skills/accessibility`
- `.agents/skills/offline-sync`
- `.agents/skills/api-contracts`
- `.agents/skills/storybook`
- `.agents/skills/playwright`
- `CONTRIBUTING.md`
- `DESIGN_SYSTEM.md`
- `ACCESSIBILITY.md`
- `CONTENT_GUIDE.md`
- `SECURITY.md`
- `LICENSES.md`
- `ADR/` decisions

Agents may create components, tests, stories, API clients, documentation, and migration plans. Agents may not alter money displays, permissions, identity flows, child-safety surfaces, justice surfaces, campaign disclosures, or emergency actions without human review.

## 7. Frontend rules for high-impact domains

### Money

Always display:

- Settled
- Pending
- Projected
- Reversed
- Disputed
- Available

Never calculate a new authoritative balance in the browser.

### Permissions

Every protected screen explains:

- Current context
- Acting identity
- Responsible OS
- Required capability
- Approval state
- Data owner

### Campaign

`mijaxx.fun` can display campaign content and submit campaign actions, but cannot control elections, MiLyfe governance, public-office authority, or `$MLY` issuance.

### Justice and legal

Documents and case states must preserve source, version, access restrictions, export, and legal-hold indicators.

### Health and care

Sensitive content is minimized, masked by default where appropriate, and never included in analytics events.

## 8. What is deliberately not selected

- No Vercel-only deployment requirement
- No hosted proprietary analytics requirement
- No multiple competing router systems
- No multiple component libraries
- No cloud-only offline sync
- No browser-side authority for money or permissions
- No hidden tracker as a growth requirement
- No frontend route that bypasses the backend Kernel
- No copied dependency on the old `milyfe.fun`, `miforge.milyfe.fun`, or `mijaxx.fun` deployments
