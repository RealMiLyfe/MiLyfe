# MiLyfe UI/UX Design System

**Status:** Design baseline
**Mode:** Frontend design only; no code
**Brand reference:** `milyfe.fun` and `miforge.milyfe.fun`
**Build rule:** The current sites are visual references only. They are not dependencies. The new product is built from scratch and must survive removal or replacement of every existing site.
**Theme:** Light-first, accessible, calm, people-centered, high-trust

## 1. Design position

MiLyfe should feel like one coherent world, not a collection of unrelated dashboards.

The interface is:

- Light
- Clear
- Human
- Useful before decorative
- Trustworthy without looking institutional
- Optimistic without making unsupported promises
- Structured enough for finance, health, justice, governance, and operations
- Simple enough for a first-time participant

The visual language should be inherited from the spirit and look of the existing MiLyfe sites, but the new system must use a new tokenized design foundation so the old websites can be taken down without breaking the product.

## 2. Brand-source rule

The current `milyfe.fun` and `miforge.milyfe.fun` sites are reference material for:

- Light visual direction
- Human-centered language
- “Add Value. Raise Quality of Life.” positioning
- Community ownership tone
- Clear calls to action
- MiForge as the economic and builder engine

The frontend must not hotlink their CSS, scripts, images, fonts, APIs, or content. The brand is recreated as owned design tokens and owned assets.

## 3. Global UI architecture

### 3.1 World shell

`milyfe.fun` becomes the conceptual world shell, even though the old website is being replaced.

The new shell provides:

- Current person or organization context
- Active cell
- OS launcher
- Universal search
- Notifications
- Receipts
- Approvals
- Support
- Privacy and consent center
- Offline status
- Accessibility controls
- Export and account controls

### 3.2 Context switcher

The user must always know whether they are acting as:

- Self
- Household member
- Caregiver
- Contributor
- Business operator
- Cooperative member
- Campaign participant
- Public-office staff member
- Community representative
- Mi agent owner

Every context change is visible and recorded when it affects an action.

### 3.3 Primary navigation

Recommended user-facing navigation:

1. **Home** — what matters now
2. **MiLyfe** — health, family, time, home, purpose, growth
3. **Earn** — work, market, money, contributions, rewards
4. **Connect** — people, community, communication, belonging
5. **Learn** — education, knowledge, research, media
6. **Build** — MiForge, ventures, services, devices, workflows
7. **Govern** — proposals, votes, campaign, election, public office
8. **Place** — Jacksonville/Duval services, mobility, emergencies, local systems
9. **Help** — support, MiResolve, legal, justice, safety

The navigation adapts to permissions but never hides the existence of support, receipts, or exit controls.

## 4. Visual design tokens

The exact values are to be extracted from the new approved brand artwork and finalized before implementation. The design system should define tokens rather than scattering visual decisions across screens.

### Color roles

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
- Informational
- Focus ring
- Disabled

The brand accent must be used intentionally. Money, health, justice, campaign, and emergency screens need semantic colors that remain accessible and do not depend only on hue.

### Type roles

- Display
- Page title
- Section title
- Card title
- Body
- Small body
- Label
- Data value
- Receipt or technical text

### Layout roles

- World shell
- Page container
- Two-column operator layout
- Single-column mobile layout
- Dashboard grid
- Timeline
- Data table
- Review panel
- Step flow
- Confirmation panel

### Component roles

- Button
- Link
- Input
- Select
- Search
- Tabs
- Card
- Stat card
- Status chip
- Approval card
- Receipt card
- Activity timeline
- Data table
- Empty state
- Offline state
- Error state
- Permission boundary
- Danger confirmation
- Export control
- Pause/revoke control

## 5. Interaction principles

### Explain before acting

Before a consequential action, show:

- What will happen
- Who will be affected
- Which OS is acting
- Which permission is being used
- Whether approval is required
- Whether money, data, health, legal, political, or physical state changes
- What can be undone
- Where the receipt will appear

### Never hide authority

Every screen has an authority indicator:

- Source of truth
- Owner
- Steward
- Responsible OS
- Support path
- Dispute path

### Separate actual from projected

For growth, money, campaigns, and rewards, the UI must visibly distinguish:

- Settled
- Pending
- Projected
- Proposed
- Approved
- Rejected
- Reversed
- Disputed

### Human approval is a product surface

Approval is not a hidden modal. It has:

- Plain-language explanation
- Evidence
- Risk level
- Alternatives
- Approve
- Reject
- Ask for review
- Delegate where allowed
- Audit receipt

## 6. MiScale UI

### Growth home

The first screen answers:

- What is growing?
- Is the growth healthy?
- What income has actually settled?
- What is projected?
- What capacity is limiting growth?
- What needs a human decision?
- What can be paused?

Top-level cards:

- Active stage
- Settled MiForge income
- Growth reserve
- Rewards settled
- Open obligations
- Capacity health
- Active ventures
- Pilot health

### Venture portfolio

Each MiForge venture is shown as a clear object with:

- Name
- Purpose
- Owner
- Contributors
- Revenue
- Costs
- Margin or current operating result
- Status
- Risk
- Capacity
- Support load
- Value-continuity record
- Next gate

### Scale map

A visual map displays the recursive network:

- MiLyfe root
- Jacksonville/Duval pilot cell
- Communities
- Organizations
- Ventures
- Services
- Devices
- Revenue flows
- Dependency flows
- Support capacity

The map must not suggest that MiLyfe owns every child cell. Ownership and stewardship are visible on every node.

### Evolution review

The user sees a before-and-after comparison for every major change:

- Current behavior
- Proposed behavior
- Affected OSes
- Affected people
- Data changes
- Permission changes
- Financial changes
- Safety changes
- Rollback plan
- Approval status

### Device contribution view

The device owner sees a plain-language contribution receipt:

- Device
- Workload
- Start and end time
- Resources used
- Data accessed
- Safety limits
- Verification state
- Reward state
- Pause
- Revoke

## 7. MiForge UI

MiForge is the main economic creation surface.

### Builder home

- Create venture
- Create service
- Create workflow
- Create agent
- Create media product
- Create education product
- Create community offer
- View active ventures
- View revenue and obligations
- View scale recommendations

### Venture creation flow

1. Need or opportunity
2. Proposed value
3. Target users or community
4. Owner and contributors
5. Delivery model
6. Costs and dependencies
7. Safety and legal review
8. Pricing or reward model
9. Pilot scope
10. Scale gate
11. Publish or pause

The flow must not promise income. It must show what is proposed and what has actually been verified.

## 8. Jacksonville / mayor campaign UI

The Campaign OS instance should support the public campaign identity represented by `mijaxx.fun`.

### Public campaign home

- Jacksonville/Duval identity
- Current reference identity: Mayor MiLyfe — Jacksonville 2027
- Candidate/campaign principal: Carnell Lee
- “We The People” positioning
- Candidate and campaign profile
- Platform
- Research
- Journey and biography
- Petition and get-involved action
- Campaign calendar
- Media
- MiLyfe join path
- Clear campaign disclaimer
- Accessibility and language controls

### Campaign operator view

- Petition and supporter pipeline
- Volunteer tasks
- Events
- Outreach consent
- Fundraising and spending records
- Disclosures
- Platform updates
- Research citations
- Media approval
- Election deadlines
- Security alerts
- Campaign-to-office transition readiness

### Political boundary

The interface must clearly distinguish:

- Campaign content
- Neutral election information
- MiLyfe governance
- Public-office administration
- Court and justice content

A campaign user cannot use Campaign OS permissions to control MiMoney, MiLyfe governance, election results, court outcomes, or public-office records.

The campaign UI can state goals and commitments. It must not display an election outcome as guaranteed.

## 9. Unified receipts and activity

Every OS uses the same receipt card pattern:

- Date and time
- Actor
- OS
- Action
- Target
- Permission used
- Approval
- Result
- Money or data impact
- Reversal or dispute path
- Export

The user can view receipts from:

- Home
- Money
- Device contributions
- Campaign
- Governance
- Care
- Justice
- MiForge
- MiScale

## 10. Accessibility and resilience

The design must include:

- Keyboard navigation
- Visible focus
- Screen-reader labels
- Reduced-motion mode
- Large-text mode
- High-contrast mode
- Captions and transcripts
- Audio description support
- Plain-language mode
- Multilingual content hooks
- Low-bandwidth mode
- Offline mode
- Print and mail-friendly views for MiJustice Inside
- Exportable receipts and records

Offline screens must say what is local, what is pending, and what cannot be completed until reconnection.

## 11. Design states

Every serious workflow needs explicit states:

- Draft
- Proposed
- Awaiting approval
- Approved
- Running
- Pending settlement
- Settled
- Needs attention
- Paused
- Reversed
- Disputed
- Appealed
- Archived
- Exported
- Removed

No blank dashboard may be mistaken for zero activity. Empty states explain whether there is no data, no permission, no connection, or no activation.

## 12. Brand uniformity across all white-label surfaces

Future branded OS surfaces may change:

- Name
- Logo
- Accent treatment
- Local language
- Public content
- Domain
- Local navigation labels

They may not change the shared:

- Receipt pattern
- Permission explanations
- Safety controls
- Export controls
- Accessibility baseline
- Dispute routing
- Money state labels
- Offline behavior
- Human approval rules

This is how the system can look local while still functioning as one accountable MiLyfe architecture.

## 13. Frontend handoff criteria

Frontend implementation begins only when the backend provides:

- Stable API contracts
- Authentication and context switching
- Permission and approval endpoints
- Receipt endpoints
- Offline status and sync state
- MiScale growth data
- MiForge portfolio data
- MiMoney settled and pending states
- Campaign data for `mijaxx.fun`
- MiKnowledge source records
- MiMedia assets and rights states
- Support and dispute routes
- Export and removal workflows

The interface is designed from the MiLyfe brand, but no existing site remains a technical dependency.
