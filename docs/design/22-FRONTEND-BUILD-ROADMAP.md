# MiLyfe Frontend Build Phases Roadmap

**Status:** Design roadmap
**Product name:** MiLyfe
**Branding:** MiLyfe light-theme system
**Primary build:** API-driven Next.js/React frontend
**No code:** This is a sequencing and acceptance design. Implementation begins only after the corresponding contracts are approved.

## 1. Objective

Build one consistent MiLyfe interface that can serve:

- People
- Households
- Contributors
- MiForge builders
- Device contributors
- Cooperatives
- Campaign participants
- Jacksonville/Duval residents
- Governance participants
- Public-office staff
- Support and justice users

The interface must feel like one world while keeping every OS independently bounded.

## 2. Frontend architecture laws

- MiLyfe is always branded and written as `MiLyfe`.
- Existing websites are references only; the new frontend is built from scratch.
- The frontend consumes the backend; it does not become the source of truth.
- Every action shows its context, authority, permission, and receipt path.
- High-impact actions require explicit human approval.
- Offline state is visible and honest.
- Money is never invented or recalculated as authoritative in the browser.
- Campaign, election, public-office, governance, legal, justice, and money surfaces remain separated.
- All primary flows work with keyboard, screen readers, reduced motion, and low bandwidth.
- A new cell or white-label presentation may change visual content but cannot remove shared safety, receipts, export, or permission controls.

## 3. Phase 0 — Product and brand freeze

### Design outputs

- Confirm the MiLyfe name and spelling everywhere
- Replace any accidental alternate product wording with `MiLyfe`
- Extract the visual direction from the existing sites without importing them
- Approve the light-theme brand tokens
- Approve type scale and spacing
- Approve logo and icon rules
- Approve voice and content style
- Approve semantic status vocabulary
- Approve accessibility baseline
- Approve campaign/public-office content boundary

### Exit gate

No frontend surface can use an unapproved brand token, old-site runtime dependency, or ambiguous product name.

## 4. Phase 1 — Repository and agent foundation

### Build design

- Frontend monorepo
- Next.js application shells
- Shared packages
- Storybook application
- API client package
- Contract package
- Brand package
- Test package
- Offline package
- Agent instructions
- License inventory
- Dependency allowlist
- CI quality gates
- MiDev OS project and repository workflow
- MiSecurity OS threat-model and release gates
- Secret, dependency, license, and publication scans
- Signed preview and release artifact requirements
- Public versus restricted frontend asset classification

### Exit gate

A new AI agent can understand the repository, find the correct contract, run the correct tests, and identify which files require human review.

## 5. Phase 2 — MiLyfe design system

### Build design

- Tokens
- Typography
- Layout primitives
- Buttons
- Inputs
- Cards
- Tables
- Tabs
- Status chips
- Modals
- Drawers
- Toasts
- Timelines
- Approval cards
- Receipt cards
- Offline banners
- Error states
- Empty states
- Permission boundaries
- Export controls
- Pause and revoke controls

### Storybook coverage

Every component needs:

- Default
- Loading
- Empty
- Error
- Disabled
- Keyboard
- Mobile
- High contrast
- Reduced motion
- Long-content
- Permission-denied
- Offline

### Exit gate

All shared components pass accessibility checks and visually use MiLyfe tokens rather than one-off styles.

## 6. Phase 3 — World shell and identity

### Build design

- MiLyfe shell
- Sign-up and sign-in
- Recovery
- Context switcher
- Active cell selector
- OS launcher
- Universal search entry
- Notifications
- Approvals
- Receipts
- Help
- Consent center
- Account export
- Account removal
- Offline status
- Business and merchant onboarding
- Service-provider, driver, creator, venture, and cooperative onboarding
- Campaign, business, and public-office context separation
- Device contribution entry
- Agent and skill enrollment entry
- Capability-wall and activation-state visibility

### Exit gate

A person, business, merchant, or campaign participant can identify who they are acting as, which context is active, what OS is involved, what permissions are being used, and how to leave or export before using domain features.

## 7. Phase 4 — Data, permissions, and offline behavior

### Build design

- Data-space browser
- Ownership labels
- Consent flows
- Delegation flows
- Permission explanations
- Receipt timeline
- Local drafts
- Pending commands
- Sync status
- Conflict review
- Retry and rollback states
- Data export package status

### Exit gate

A user can complete a permitted offline action, see that it is pending, reconnect, understand whether it succeeded, and access the final receipt.

## 8. Phase 5 — Core MiLyfe home and personal surfaces

### Build design

- MiLyfe home
- MiHealth entry
- MiFamily entry
- MiBelong entry
- MiTime entry
- MiHome entry
- MiPurpose entry
- MiWork entry
- MiEducation entry
- MiWealth and MiFinance entry
- MiCare entry

These are navigation and user journeys first. Each OS retains its own data, authority, and support boundaries.

### Exit gate

The home experience is useful without becoming a giant undifferentiated dashboard. Each action routes to the correct OS and authority.

## 9. Phase 6 — MiForge and MiScale first-income surfaces

This is the first economic growth frontend and should be built before broad decorative expansion.

### MiForge surfaces

- Builder home
- Create venture
- Create service
- Create agent
- Create workflow
- Create media product
- Create education product
- Venture portfolio
- Contributor roles
- Value contract
- Delivery status
- Revenue status
- Costs and obligations
- Publish, pause, and retire

### MiScale surfaces

- Growth home
- Active stage
- Settled versus projected income
- Rewards owed versus settled
- Capacity health
- Operating reserve
- MiForge portfolio health
- Device contribution status
- Scale gates
- Evolution proposals
- Replication readiness
- Value continuity register

### Exit gate

The UI can display the MiForge-to-MiScale flywheel without creating false money, hiding obligations, or confusing projected income with settlement.

## 10. Phase 7 — Device contributions and rewards

### Build design

- Device enrollment
- Owner authorization
- Workload explanation
- Resource and power display
- Safety limits
- Pause and revoke
- Contribution verification
- Reward status
- Device receipt
- Dispute route

### Exit gate

A device owner can understand and control every contribution. No device can silently become a worker, sensor, or compute source.

## 11. Phase 8 — Campaign and mayor-campaign surfaces

### Public `mijaxx.fun` experience

- Jacksonville/Duval identity
- Mayor MiLyfe — Jacksonville 2027 profile
- Candidate/campaign principal: Carnell Lee
- “We The People” positioning
- Platform
- Research
- Journey and biography
- Petition and get-involved flows
- Campaign calendar
- Media
- MiLyfe join path
- Accessibility and language controls
- Campaign disclaimer and public-record boundary

### Campaign operator experience

- Supporter consent
- Volunteer tasks
- Events
- Petition tracking
- Outreach
- Contributions
- Spending
- Disclosures
- Research citations
- Media approval
- Security
- Election deadlines
- Transition readiness

### Political boundary

The interface can represent campaign goals and commitments. It must not represent a mayoral or presidential result as guaranteed, and it must not merge Campaign OS with MiElection or MiPublic Office.

### Exit gate

The public campaign website can be replaced or moved without losing the campaign identity, content history, receipts, or records.

## 12. Phase 9 — MiMoney and economic interfaces

### Build design

- Wallet/account view
- `$MLY` balance states
- Settled and pending transactions
- Contributions
- Rewards
- Refunds
- Reversals
- Treasury proposals
- Statements
- Books and tax records
- Mutual pools
- Marketplace transactions
- Financial support and disputes

### Exit gate

Every visible amount comes from an authoritative backend state and is labeled correctly. The frontend never creates balances or bypasses MiMoney.

## 13. Phase 10 — Knowledge, media, and communication

### Build design

- MiKnowledge spaces
- Source-linked documents
- Search
- Version history
- Corrections
- MiMedia channels
- Audio/video publishing
- Captions and transcripts
- Media rights state
- MiComm messages
- Notifications
- Campaign and public-office publishing boundaries

### Exit gate

Users can tell whether they are reading a source record, a knowledge summary, a media publication, a campaign statement, or an AI-generated explanation.

## 14. Phase 11 — Governance, legal, justice, and public office

### Build design

- Governance proposals
- Votes and participation
- MiResolve cases
- MiLegal source and contract views
- MiJustice case organization
- Redress workflows
- Inside accessibility and print views
- MiElection information surfaces
- MiPublic Office profile
- Presidency role profile
- Campaign-to-office transition interface

### Exit gate

Internal platform disputes, neutral legal infrastructure, rights/court work, election information, and public-office administration remain visibly separate.

## 15. Phase 12 — Jacksonville/Duval place experience

### Build design

- Local service directory
- Place map
- Housing
- Transit
- Food
- Energy
- Water
- Cleaning and recycling
- Repair and maintenance
- Public health
- Emergency resources
- Local ventures
- Community projects
- Civic requests
- Local support

### Exit gate

A Jacksonville/Duval resident can use place services without needing to understand the entire architecture. The system still shows which OS owns each service and which support route applies.

## 16. Phase 13 — Production hardening

### Required testing

- Chromium, Firefox, and WebKit
- Mobile and desktop breakpoints
- Keyboard-only journeys
- Screen-reader review
- High contrast
- Reduced motion
- Slow network
- Offline and reconnect
- Permission denial
- Revocation
- Session recovery
- Data export
- Receipt visibility
- Campaign/public-office separation
- Money state accuracy
- Visual regression
- Performance budgets
- Error recovery
- Security headers
- Dependency audit

Playwright is appropriate for multi-browser journeys because it supports Chromium, Firefox, and WebKit through one API. Storybook is the component workshop and visual contract. The two are used together rather than treating screenshots as the only quality measure.

## 17. Phase 14 — Controlled replication

Only after Jacksonville/Duval passes the production gate:

- Export the frontend configuration package
- Export local content and translation packages
- Apply a new cell identity
- Apply new local policy profiles
- Apply local brand overrides where permitted
- Connect to the same backend contracts
- Test local permissions and data separation
- Test offline behavior
- Test removal and fork behavior

The visual experience can be local, but receipts, permissions, accessibility, export, and safety cannot be removed.

## 18. Definition of frontend readiness

The frontend is ready for controlled public use when:

- It uses MiLyfe consistently everywhere.
- It has no dependency on the old websites.
- It consumes stable backend contracts.
- It shows authoritative versus projected states.
- It supports context, permissions, receipts, offline behavior, and export.
- It passes accessibility and browser tests.
- It protects sensitive data in rendering, caching, logs, and analytics.
- It separates campaign, election, public office, governance, legal, justice, health, and money surfaces.
- It can be maintained by an AI agent under human review.
- It can evolve without breaking the MiLyfe brand or authority model.
