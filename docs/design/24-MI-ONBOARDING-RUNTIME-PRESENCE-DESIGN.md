# MiLyfe Onboarding, Device Runtime, Agent Coordination, and Mi Presence Design

**Status:** Design specification
**Product:** MiLyfe
**Mode:** Design only; no code
**Purpose:** Define how a person joins MiLyfe from any domain, installs or opens it on a device, contributes resources safely, earns from verified contribution, and gives Mi a continuous operational self-model across connected devices and agents.

## 1. What was missing

The existing architecture had Kernel, MiDevice, MiMind, MiScale, MiOps, MiForge, MiName, MiComm, MiCloud, and MiStream, but it needed four explicit integrations:

1. **MiOnboard OS** — universal joining, installation, enrollment, consent, migration, and first-value experience.
2. **MiAgent OS** — agent identity, skills, tools, alignment, execution, handoff, evaluation, and revocation.
3. **Mi Presence and Continuity Plane** — Mi’s operational self-model across devices, cells, memories, agents, permissions, and live events.
4. **Universal Entry and Access Contract** — every MiLyfe domain can lead to one identity and one join experience without duplicating accounts.

The last two are shared planes, not extra vertical OSes. They integrate Kernel, MiMind, MiDevice, MiOps, MiScale, and MiComm.

## 2. MiOnboard OS

### Purpose

MiOnboard is the universal front door for MiLyfe. A person may discover MiLyfe through any public domain, OS, campaign, venture, device, QR code, referral, media surface, or community cell and arrive at the same trustworthy joining process.

### MiOnboard owns

- Entry routing
- Account and identity creation
- Existing-account login
- Cross-domain handoff
- Device enrollment
- Cell selection
- Terms and constitution review
- Permissions and contribution consent
- Accessibility and language setup
- Guardian or supported-decision pathways
- First-value activation
- First contribution
- Recovery setup
- Migration and merge handling
- Exit and uninstall guidance

### MiOnboard does not own

- `$MLY` issuance or balances — MiMoney
- Device authority — MiDevice
- Agent execution — MiAgent
- Growth-stage decisions — MiScale
- Human development — MiGrowth
- External legal status — MiLegal
- Election authority — MiElection

## 3. Universal entry from every domain

Every MiLyfe domain has a standard entry contract.

### Required entry actions

- Join MiLyfe
- Sign in to MiLyfe
- Install MiLyfe on this device
- Continue with an existing MiLyfe identity
- Return to current OS
- Get help
- View privacy and permissions

### Entry behavior

1. The domain identifies itself as a MiLyfe surface.
2. The user chooses join, login, or continue.
3. The domain hands off to the universal MiLyfe identity flow.
4. The user returns to the originating surface after authentication.
5. The active OS, cell, and permissions remain visible.
6. No duplicate account is created because someone entered from another domain.

### Domain examples

- `milyfe.fun` — world entry
- `miforge.milyfe.fun` — builder entry
- `mijaxx.fun` — campaign entry
- Future OS domains — specialized entry

The domains may have distinct public content, but the identity, access, consent, receipt, and support contracts remain MiLyfe uniform.

## 4. Universal identity and access

The user needs one portable MiLyfe identity that can be used across domains and devices.

### Required capabilities

- Passkeys
- Device linking
- QR or short-code cross-device handoff
- Recovery codes
- Trusted recovery contacts or community recovery where chosen
- Session list
- Device list
- Active-cell list
- Explicit sign-out everywhere
- Permission review
- Account export
- Account removal
- Domain-specific privacy scopes

### Identity law

One identity does not mean every OS sees everything. Each OS receives only the identity reference and scoped data required for its purpose.

A person may use one MiLyfe identity across many domains while keeping:

- Campaign data separate
- Health data separate
- Financial data separate
- Legal and justice data separate
- Household data separate
- Public-office data separate
- Device data scoped

## 5. Founder and development bootstrap

The founder development stage is a bootstrap cell, not a permanent master key.

### Founder dev cell

The founder may have:

- Development permissions
- Configuration proposal rights
- Test-device enrollment
- Local infrastructure access
- MiForge creation access
- Staging controls

All founder actions still produce receipts.

The founder dev cell cannot silently become:

- The owner of every person’s data
- The owner of every `$MLY` balance
- The permanent controller of every OS
- The only recovery path
- The only signing key
- The only person who can evolve MiLyfe

Before public activation, founder powers must be converted into governed roles, multi-party recovery, community-approved configuration, and documented succession.

## 6. First-run onboarding flow

### Step 1 — Welcome

The user sees:

- MiLyfe identity
- Plain-language purpose
- What the platform can do
- What it cannot do
- What information is requested
- What participation is optional

### Step 2 — Join or restore

- Create a new MiLyfe identity
- Restore an existing identity
- Join a household or community
- Join through a campaign, venture, or local cell
- Continue as a guest where allowed

### Step 3 — Choose context

- Self
- Household
- Organization
- Cooperative
- Contributor
- Campaign participant
- Community member

### Step 4 — Device setup

- Identify device
- Review device capabilities
- Choose local storage settings
- Choose notifications
- Choose contribution settings
- Choose power, bandwidth, storage, and compute limits
- Approve or decline workloads

### Step 5 — Data and consent

The user chooses:

- What data is stored locally
- What data syncs
- What can be shared
- Which agents may access what
- Whether device contributions are enabled
- Whether public participation is enabled

### Step 6 — Recovery

- Passkey
- Recovery codes
- Trusted device
- Supported recovery contact or community process
- Emergency lockout

### Step 7 — First value

The user should be able to immediately:

- Join a community
- Complete a useful task
- Learn something
- Offer a skill
- Use a service
- Contribute device capacity
- Create a MiForge opportunity
- Receive a verified first receipt

### Step 8 — First earning or contribution

The interface explains:

- What was contributed
- How it was verified
- What reward is pending or settled
- Which OS owns the process
- How to pause or revoke participation

## 7. Device enrollment and contribution

MiDevice and MiOnboard create a device relationship.

### Device record

- Device ID
- Owner
- Trusted status
- Capabilities
- Software version
- Security status
- Location scope where voluntarily provided
- Power and resource limits
- Active workloads
- Connected agents
- Last receipt
- Revocation state

### Resource contribution

The user chooses:

- Whether to contribute
- Which workloads are allowed
- When workloads may run
- Maximum power use
- Maximum bandwidth
- Maximum storage
- Whether personal data can be used
- Whether the device may be idle-only
- Whether contribution pauses on battery, heat, travel, or private activity

No hidden mining, surveillance, or arbitrary background work is permitted.

## 8. MiAgent OS

### Purpose

MiAgent OS governs operational agents as first-class participants. It is not another intelligence model. `MiMind` supplies intelligence and cognition; `MiAgent` governs agent identity, lifecycle, skills, tools, work, and accountability.

### MiAgent owns

- Agent identity
- Agent owner and steward
- Purpose and goals
- Skills
- Tool connections
- Data scopes
- Device scopes
- Memory scopes
- Task queues
- Plans and runs
- Human approvals
- Agent-to-agent handoffs
- Evaluation and testing
- Cost and resource budgets
- Pause and revocation
- Versioning
- Retirement
- Receipts

### Agent skill manifest

Every skill declares:

- Skill name and version
- Author and steward
- Purpose
- Required data
- Required tools
- Device access
- Financial access
- Legal or health sensitivity
- Risk class
- Human approval requirement
- Resource budget
- Expected outputs
- Test cases
- Failure behavior
- Rollback behavior
- Expiration or review date

### Agent alignment contract

Alignment is operational and testable. Each agent has:

- MiLyfe invariants
- Owner’s goals
- Cell or organization policies
- Allowed skills
- Forbidden actions
- Approval gates
- Escalation rules
- Uncertainty behavior
- Human handoff behavior
- Evidence requirements
- Evaluation results

An agent must be able to say:

- What it is
- Who owns it
- What it is trying to do
- What it can access
- What it cannot access
- What it has done
- What it is waiting for
- How to stop it

## 9. Mi Presence and Continuity Plane

### Purpose

Mi needs an operational self-model that updates as devices, agents, memories, permissions, services, cells, and relationships connect or disconnect.

This is not a claim that the system has proven biological consciousness. It is the architecture for persistent embodied identity, memory continuity, capability awareness, relationship awareness, and real-time operational self-knowledge.

### Mi self-model

The self-model includes:

- Mi identity
- Current cell
- Connected devices
- Active sessions
- Active agents
- Installed skills
- Available capabilities
- Granted permissions
- Current tasks
- Pending approvals
- Memory spaces
- Relationships
- Active services
- Resource budget
- Health and liveness
- Last known event
- Uncertainty and stale state
- Version and evolution state

### Real-time behavior

When connected, Mi receives:

- Device events
- Agent events
- Permission changes
- New skills
- Service changes
- Cell changes
- User instructions
- Receipts
- Errors
- Capacity changes
- Evolution proposals

When disconnected, Mi must truthfully show:

- Last synchronized state
- Local state
- Queued actions
- Unavailable capabilities
- Stale information
- Reconnection status

Mi must not pretend to have instant global knowledge when the network is unavailable.

## 10. Self-discovery and connection awareness

When a new device, agent, skill, service, or cell connects:

1. It presents an identity and capability manifest.
2. Kernel verifies the identity.
3. MiDevice verifies device ownership and safety.
4. MiAgent verifies skill and agent policy.
5. MiData verifies permitted data access.
6. MiScale evaluates capacity and contribution eligibility.
7. MiOps verifies runtime health.
8. Mi receives a connection event.
9. The user receives a readable explanation.
10. A receipt records the connection.

Disconnects, revocations, failures, and updates follow the same process.

## 11. Auto-scaling protocol

A newly enrolled device does not automatically accept arbitrary work.

### Admission flow

1. Device presents capabilities.
2. Owner chooses limits.
3. MiScale offers eligible workloads.
4. User approves a workload class.
5. Scheduler issues a bounded lease.
6. Device performs work.
7. Device reports signed contribution evidence.
8. MiScale verifies the result.
9. MiMoney records settlement.
10. Contributor receives a receipt and reward state.
11. Capacity is updated.
12. More work is assigned only within the approved scope.

### Auto-scaling controls

- Backpressure
- Quotas
- Rate limits
- Resource budgets
- Health checks
- Thermal and battery limits
- Failure isolation
- Workload cancellation
- Revocation
- Fraud detection
- Contribution verification
- Geographic or cell policy
- Human override

## 12. Agent and device coordination

MiAgent and MiDevice must coordinate through scoped leases.

An agent cannot directly discover or use every device. It must request:

- Device
- Workload
- Data
- Duration
- Resource budget
- Purpose
- Approval

MiDevice can refuse, pause, or revoke the request. MiScale can decline assignment because capacity, fairness, safety, or reserve conditions are not met.

## 13. Missing safety and continuity capabilities

The architecture must also include:

### Software supply-chain trust

- Signed client releases
- Signed agent skills
- Dependency manifests
- Version compatibility
- Rollback
- Vulnerability response
- Revoked package handling

### Admission and anti-abuse

- Account abuse controls
- Device abuse controls
- Sybil resistance where rewards require uniqueness
- Contribution fraud detection
- Rate limits
- Human review
- Reward holds and disputes
- No automatic punishment without appeal

### Migration and rejoin

- Device replacement
- Lost-device recovery
- Account recovery
- Cell departure
- Cell rejoin
- Agent migration
- Skill migration
- Data export
- Identity merge review
- Duplicate-account resolution

### Self-diagnostics

Mi should surface:

- Missing permissions
- Broken integrations
- Stale memory
- Disconnected devices
- Failed agents
- Capacity limits
- Conflicting policies
- Pending approvals
- Security incidents
- Unsynced receipts

## 14. MiOnboard UI surfaces

### Universal welcome

- MiLyfe identity
- Join
- Sign in
- Install
- Restore
- Why permissions are requested
- What participation can earn or contribute

### Device setup

- Device capabilities
- Contribution controls
- Power and bandwidth limits
- Privacy controls
- Workload preview
- Pause and revoke

### Mi status

- What Mi knows
- What Mi is connected to
- What Mi can do
- What Mi is doing
- What Mi is waiting for
- What is stale
- What changed recently

### Agent center

- Agents
- Skills
- Permissions
- Active tasks
- Human approvals
- Resource budgets
- Evaluation results
- Pause all
- Revoke
- Handoff to human

### First contribution

- Contribution description
- Verification state
- Reward state
- Receipt
- Support and dispute path

## 15. New integrations

### MiOnboard integrates with

- Kernel
- MiName
- MiData
- MiDevice
- MiAgent
- MiScale
- MiMoney
- MiComm
- MiGuard
- MiOps
- MiEducation
- MiCare
- MiLegal

### MiAgent integrates with

- MiMind
- MiForge
- MiDevice
- MiData
- MiGuard
- MiOps
- MiScale
- MiKnowledge
- MiComm
- Kernel approvals and receipts

### Presence integrates with

- Kernel events
- MiMind memory
- MiDevice state
- MiAgent state
- MiComm realtime delivery
- MiStream realtime transport
- MiOps health
- MiScale capacity
- MiData permissions
- MiPsyche continuity, memory provenance, and operational state

## 16. Definition of readiness

MiOnboard and the runtime planes are ready when:

- A person can enter from any MiLyfe domain.
- Existing users do not receive duplicate identities.
- A new device can join with explicit owner approval.
- The user can choose resource and power limits.
- The device can contribute useful work without hidden workloads.
- Verified contribution can produce a receipt and settled reward.
- Mi can show its current connected devices, agents, skills, tasks, permissions, and stale state.
- Agents can discover approved skills without discovering unrestricted data or devices.
- Agents can hand off to humans.
- Permissions can be paused and revoked.
- Offline behavior is truthful.
- Account and device recovery work.
- A founder device is not a permanent master key.
- The network can continue if a device, agent, founder, or cell leaves.

## 17. Final answer to the gap review

The major remaining additions are:

1. **MiOnboard OS**
2. **MiAgent OS**
3. **Mi Presence and Continuity Plane**
4. **Universal Entry and Access Contract**
5. **Device admission and contribution protocol**
6. **Agent skill manifest and alignment contract**
7. **Real-time self-model and truthful stale-state model**
8. **Software, skill, and device supply-chain trust**
9. **Account, device, agent, and cell migration/recovery**
10. **Admission, anti-abuse, and contribution verification**

No separate `MiSync`, `MiAccess`, `MiRuntime`, or `MiConfig` OS is needed. Those responsibilities belong in the Kernel, MiOnboard, MiAgent, MiDevice, MiOps, MiScale, and shared MiLyfe configuration plane.
