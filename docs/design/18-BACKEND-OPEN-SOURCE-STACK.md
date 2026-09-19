# MiLyfe Backend Open-Source Stack and Build Design

**Status:** Backend architecture selection
**Constraint:** $0 software budget; self-hosted/open-source first
**Implementation rule:** No stubs, fake endpoints, placeholder business logic, or unreviewed security shortcuts
**Frontend:** Deferred until the backend contracts and operational baseline are complete
**Brand source:** `milyfe.fun`; the later frontend will use its light-theme brand system

## 1. Decision summary

No single GitHub repository contains the complete MiLyfe backend. The correct approach is a small number of mature open-source infrastructure projects plus a real MiLyfe domain backend.

The first backend should be a **modular monolith with strong OS boundaries**, not dozens of microservices. Each OS is an independently owned module with its own data ownership, permissions, APIs, events, receipts, tests, and removal plan. The modules share one Kernel contract and one controlled database boundary at the beginning. They can split into services later only when there is a demonstrated operational reason.

### Recommended baseline

- **Platform foundation:** self-hosted Supabase stack using PostgreSQL, Auth, Storage, Realtime, and Functions where appropriate.
- **MiLyfe API:** custom TypeScript/NestJS modular backend. Supabase is infrastructure, not the source of MiLyfe domain authority.
- **Authorization:** PostgreSQL Row-Level Security for hard data isolation plus OpenFGA for relationship and delegation rules.
- **Events:** PostgreSQL transactional outbox first; NATS JetStream when the pilot needs durable multi-process or multi-cell fanout.
- **Long-running workflows:** application workflows first; Temporal only for workflows that truly need durable timers, retries, compensation, or multi-day state.
- **Search and AI retrieval:** PostgreSQL full-text search plus pgvector first; separate search infrastructure only when measured need exists.
- **Files:** Supabase Storage for the first backend; SeaweedFS or another S3-compatible layer only when media volume requires it.
- **Operations:** Docker or Podman Compose, reverse proxy, encrypted backups, OpenTelemetry, Prometheus, and Grafana.
- **Deployment control panel:** Coolify is optional. It manages infrastructure supplied by MiLyfe; it is not free hosting.
- **External extensions:** Apache Fineract, Mojaloop, ERPNext, and PeerTube are adapters or later domain deployments, never hidden sources of truth for Kernel, `$MLY`, or governance.

## 2. Free means no software license fee, not zero operational responsibility

A $0 launch is possible for development, a small controlled pilot, or a deployment on hardware that MiLyfe already owns or receives from a community partner. It is not honest to promise unlimited, highly available, backed-up, public production service at no infrastructure cost.

The design must explicitly account for:

- Compute
- Power
- Network connectivity
- Domain and DNS
- Email and phone delivery
- Storage growth
- Backups in a second location
- Security response
- Human support
- Legal and professional review
- Financial and health operations

Coolify's documentation explicitly places server, operating-system, DNS, secrets, data, and backup responsibility on the operator when self-hosting. Supabase's self-hosting documentation likewise distinguishes the local development stack from production self-hosting and notes that managed backups and point-in-time recovery are not included in the self-hosted platform. These are design constraints, not reasons to abandon open source.

## 3. Repository selection

### 3.1 Selected foundation: Supabase self-hosted

Repository: <https://github.com/supabase/supabase>

Official documentation describes Supabase as a PostgreSQL-centered open-source platform with self-hosting through Docker. Its architecture includes PostgreSQL, authentication, REST and GraphQL access, realtime, storage, and server-side functions. The official self-hosting guide provides a pinned Docker deployment path and explicitly distinguishes production self-hosting from the local CLI stack.

Why it fits MiLyfe:

- PostgreSQL is appropriate for relational OS data, receipts, contracts, and accounting invariants.
- Transactions are necessary for money, approvals, receipts, and state transitions.
- Row-Level Security can enforce cell and ownership boundaries at the database edge.
- Storage and realtime reduce the amount of infrastructure required for the first pilot.
- The project has explicit AI-agent instructions and skills in its repository, which is useful as a model for our own agent-ready repository.

Required safeguards:

- Pin versions; never deploy directly from moving `main`.
- Use the production self-hosting path, not `supabase start` exposed to the Internet.
- Generate unique secrets and rotate them.
- Build an independent backup and restore process.
- Keep the MiLyfe API as the authority for domain commands.
- Do not expose service-role credentials to clients.
- Do not treat autogenerated REST APIs as a substitute for authorization design.

### 3.2 Alternative, not a second foundation: Appwrite

Repository: <https://github.com/appwrite/appwrite>

Appwrite's official materials describe a self-hostable backend containing authentication, databases, storage, functions, messaging, hosting, and realtime under a BSD-3-Clause license. It is a credible alternative for teams wanting an all-in-one backend platform.

Decision: **Do not run Supabase and Appwrite together for the same core backend.** Appwrite can be evaluated as an alternative or used by a future independent cell, but running both would duplicate identity, data, storage, and event responsibilities.

Supabase is preferred for MiLyfe's first backend because PostgreSQL-native schemas, transactions, RLS, and ledger-oriented relational modeling are central to the architecture.

### 3.3 Identity: start with Supabase Auth; preserve OIDC portability

The first installation should use self-hosted Supabase Auth to avoid two competing identity systems.

The API must still implement an identity-provider boundary so a later cell can use Keycloak or another OIDC provider without changing MiLyfe entity IDs or domain ownership.

Keycloak repository: <https://github.com/keycloak/keycloak>

Keycloak remains a strong later option for independent realms, identity federation, enterprise SSO, and multi-cell deployments. It must not be added merely because it is popular; running both Keycloak and Supabase Auth from day one would create duplicate accounts and recovery paths.

### 3.4 Authorization: OpenFGA plus database enforcement

Repository: <https://github.com/openfga/openfga>

OpenFGA describes itself as an open-source, fine-grained authorization engine inspired by Zanzibar, with relationship-based and attribute-based authorization concepts. It is a good match for household, cooperative, campaign, public-office, caregiver, device, and delegated-authority relationships.

Use it for questions such as:

- Can this caregiver view this care plan?
- Can this campaign staff member publish this campaign asset?
- Can this cooperative treasurer approve this treasury action?
- Can this Mi agent request a tool on behalf of this person?
- Can this cell receive a bridge event from another cell?

Do not rely on OpenFGA alone. PostgreSQL RLS must still prevent accidental cross-cell data access. The API must also enforce action risk classes, approvals, and receipts.

### 3.5 Database AI retrieval: pgvector

Repository: <https://github.com/pgvector/pgvector>

pgvector provides vector similarity search inside PostgreSQL. It is appropriate for the first MiKnowledge and MiMind retrieval layer because embeddings, source records, permissions, provenance, and deletion rules can remain close to the authoritative data.

The first design should use:

- PostgreSQL full-text search for exact and lexical search
- pgvector for semantic retrieval
- Source IDs and permission checks on every result
- Separate personal, organizational, and public knowledge spaces
- No retrieval of data merely because an embedding exists

### 3.6 Events: PostgreSQL outbox first; NATS later

NATS repository: <https://github.com/nats-io/nats-server>

The first release should use a transactional outbox in PostgreSQL. A command and its receipt are committed atomically; a worker publishes an event after commit. This keeps the initial $0 deployment understandable and makes database recovery simpler.

NATS JetStream can be added when:

- Multiple backend processes need durable fanout
- A cell needs local event replay
- Federation requires bridge delivery
- Media and notification workloads need independent consumers

Do not introduce Kafka or a large event platform before the outbox has demonstrated a real limit.

### 3.7 Workflows: do not begin with Temporal

Temporal repository: <https://github.com/temporalio/temporal>

Temporal is a serious candidate for durable, retryable, long-running workflows. It is not necessary for every request and adds operational weight.

Use application workflows first for ordinary actions. Introduce Temporal only for processes such as:

- Long-running legal cases
- Multi-step redress and restitution
- Campaign-to-public-office transition
- Emergency coordination with deadlines
- Financial settlement workflows that require compensation and retries
- Federated synchronization with durable timers

### 3.8 Observability: OpenTelemetry, Prometheus, Grafana

Repositories:

- <https://github.com/open-telemetry/opentelemetry-collector>
- <https://github.com/prometheus/prometheus>
- <https://github.com/grafana/grafana>

Use OpenTelemetry for traces and structured telemetry, Prometheus for metrics, and Grafana for operational dashboards. Do not send private content, health data, legal documents, or financial payloads into telemetry by default.

Every event and request must carry a correlation ID, but observability data must be separately permissioned and redacted.

### 3.9 Deployment: Docker or Podman Compose; Coolify optional

Repositories:

- <https://github.com/podman-container-tools/podman>
- <https://github.com/coollabsio/coolify>
- <https://github.com/traefik/traefik>

Docker Compose is the simplest first deployment target because upstream Supabase supplies a Compose-based self-hosting path. Podman is a credible rootless alternative. Traefik can provide ingress and automatic certificates when the deployment has a real domain and public server.

Coolify can later provide a dashboard and Git-based deployment workflow. It does not supply compute, backup, DNS, or security operations.

### 3.10 Domain extensions

#### Apache Fineract

Repository: <https://github.com/apache/fineract>

Official Apache materials describe Fineract as an open-source, cloud-ready core banking platform with open APIs, savings, loans, client management, accounting, and reporting capabilities.

Use only as a potential MiCredit/MiBank extension after legal and operational review. Fineract must not become the authority for internal `$MLY` issuance or the complete MiMoney design.

#### Mojaloop

Repository: <https://github.com/mojaloop/project>

Mojaloop's official project materials describe an open-source interoperable payment platform with a central ledger and provider adapters. Its own FAQ distinguishes interoperability from wallet software.

Use it only as an optional external-bridge or provider-interoperability project. Do not use it as the internal `$MLY` ledger.

#### ERPNext

Repository: <https://github.com/frappe/erpnext>

ERPNext is a mature open-source ERP candidate with accounting, inventory, manufacturing, CRM, projects, HR, and related business functions.

Use it as an optional business or manufacturing system connected through adapters. Do not make it the Kernel, the MiMoney authority, or the source of truth for every MiLyfe OS.

#### PeerTube

Repository: <https://github.com/Chocobozzz/PeerTube>

PeerTube is an ActivityPub-federated video platform with P2P delivery and an AGPL license. It is a strong later implementation for the video portion of MiMedia, not a replacement for the full MiMedia OS, MiStory, MiKnowledge, or Campaign OS.

#### GrowthBook and flagd

Repositories:

- <https://github.com/growthbook/growthbook>
- <https://github.com/open-feature/flagd>

These are optional MiScale extensions for controlled feature rollout, staged activation, experimentation, and evolution. Start with one flag system. `flagd` is the lighter rollout service; GrowthBook is the later experimentation and product-analytics option. Neither may silently change permissions, money rules, legal status, or reserved actions.

#### CiviCRM

Repository: <https://github.com/civicrm/civicrm-core>

CiviCRM is an optional campaign and nonprofit CRM adapter for contacts, memberships, donations, events, and constituent workflows. It must not become the MiLyfe identity authority, MiMoney ledger, election authority, or Campaign OS source of truth. Any integration must map records through explicit MiLyfe contracts and respect campaign-data separation.

## 4. Backend architecture

### 4.1 One modular monolith first

The backend is organized by bounded modules, not by a web of early microservices.

Suggested repository layout:

- `apps/api` — MiLyfe API and command/query boundary
- `apps/worker` — outbox, scheduled jobs, media jobs, notifications, reconciliation
- `packages/contracts` — OpenAPI, JSON Schema, event schema, receipt schema
- `packages/policy` — risk classes, approval rules, reserved-action rules
- `packages/sdk` — generated clients for future web and mobile frontends
- `db/migrations` — versioned schema changes
- `db/seed` — only deterministic development and test fixtures
- `infra/compose` — pinned infrastructure deployment
- `infra/backup` — encrypted backup and restore procedures
- `ops/dashboards` — redacted metrics and operational dashboards
- `docs/adr` — architecture decisions
- `.agents/skills` and `AGENTS.md` — instructions for AI coding agents
- `tests/contract` — cross-OS contracts
- `tests/integration` — real database and service integration
- `tests/security` — authorization and isolation tests
- `tests/property` — ledger and invariant tests

### 4.2 Database boundaries

Use PostgreSQL schemas or clearly isolated module namespaces:

- `kernel`
- `entities`
- `identity`
- `onboarding`
- `agent`
- `presence`
- `psyche`
- `capabilities`
- `data`
- `records`
- `receipts`
- `events`
- `money`
- `commerce`
- `scale`
- `care`
- `knowledge`
- `media`
- `campaign`
- `election`
- `public_office`
- `governance`
- `legal`
- `justice`
- `ops`

A module may reference another module only through a documented contract. It may not write directly into another module's source-of-truth tables.

### 4.3 Kernel backend responsibilities

The Kernel backend must provide:

- Entity creation and lifecycle
- Identity references
- Cell and scope context
- Capability issuance
- Permission checks
- Delegation and revocation
- Approval requests
- Risk classification
- Receipts
- Events
- Idempotency
- Offline replay handling
- Export jobs
- Removal jobs
- Fork manifests
- Service registry
- Correlation and audit IDs

### 4.4 MiData responsibilities

MiData must provide:

- Data ownership and stewardship records
- Purpose-bound access
- Consent records
- Retention and deletion
- Export packages
- Data lineage
- Cross-OS data contracts
- Restricted data categories
- Subject access workflows
- Correction workflows
- Legal holds
- Data-space membership

### 4.5 MiMoney responsibilities

MiMoney is not a thin payment feature. It needs a deliberately separate, invariant-tested accounting core:

- Account and wallet ownership
- Immutable journal entries
- Double-entry or equivalent balanced postings
- Available and pending balances
- No negative balance invariant
- Idempotency keys
- Settlement states
- Holds and releases
- Refunds and reversals
- Reconciliation
- Treasury permissions
- Cooperative and mutual controls
- Dispute links
- Exportable statements
- Ledger integrity verification
- Clear separation between internal `$MLY` and external currency

The first release must not claim to operate regulated external financial products merely because the internal ledger works.

### 4.6 Receipts and events

Every command must produce a receipt with:

- Actor
- Cell
- OS
- Action
- Target
- Scope
- Approval
- Risk class
- Before and after references
- Timestamp
- Correlation ID
- Reversal or correction path
- Dispute and legal route

Events should be committed through a transactional outbox. No event may be emitted as if successful before the authoritative transaction commits.

## 5. AI-agent configuration standard

The repository must be designed for an AI agent without allowing the agent to bypass human review.

Required files and controls:

- `AGENTS.md` at the repository root
- Nested `AGENTS.md` files for each major module
- `.agents/skills/` with one skill per OS and one for database changes
- `CONTRIBUTING.md`
- `SECURITY.md`
- `THREAT_MODEL.md`
- `LICENSES.md`
- `ARCHITECTURE.md`
- Architecture decision records
- OpenAPI and JSON Schema as source contracts
- Database migration rules
- Required test commands
- Forbidden shortcuts
- No service-role credentials in client code
- No destructive migrations without explicit approval
- No changes to money, identity, permissions, health, child, legal, or justice modules without human review
- Human sign-off for high-impact behavior

AI agents should be allowed to:

- Inspect the repository
- Generate complete migrations
- Generate contract tests
- Run local integration tests
- Update documentation
- Produce implementation plans
- Propose changes
- Prepare pull requests

AI agents should not be allowed to:

- Deploy directly to production
- Rotate or reveal secrets
- Approve their own security changes
- Change money invariants silently
- Expand a capability scope without approval
- Disable audit receipts
- Delete records or users without an approved policy
- Claim legal, financial, health, or election authority

## 6. Backend build order

### Phase A — Repository and contracts

Deliver:

- Repository structure
- License inventory
- Dependency allowlist
- Architecture decision records
- OS module map
- OpenAPI base
- Event and receipt schemas
- Entity and cell model
- Agent instructions
- CI quality gates

No product feature is accepted before this phase is complete.

### Phase B — Runtime and database

Deliver:

- Pinned Compose deployment
- PostgreSQL
- Supabase services
- Secrets management
- Database migrations
- Health checks
- Backup and restore
- Local development profile
- Test profile
- Production-like profile
- Ingress and TLS profile

### Phase C — Kernel

Deliver:

- Authenticated identity
- Cell context
- Entity lifecycle
- Capabilities
- RLS
- OpenFGA model
- Approvals
- Receipts
- Events
- Idempotency
- Export
- Removal
- Fork manifest

### Phase D — Data and safety

Deliver:

- MiData
- Records subsystem
- Consent
- Retention
- Data export
- Caregiver delegation
- Device registry
- Device scopes
- MiGuard policies
- Security incident records

### Phase E — MiMoney and economy

Deliver:

- Ledger and invariants
- Wallet/account ownership
- Settlement and reconciliation
- MiMutual
- Treasury controls
- Commerce integration
- Books and tax records
- Credit and capital boundaries
- Financial support and disputes

### Phase F — Knowledge, media, AI, and communication

Deliver:

- MiKnowledge
- MiMedia
- MiComm
- MiStream adapters
- MiSearch
- pgvector retrieval
- Source provenance
- AI memory permissions
- AI tool scopes
- Campaign content integration
- `mijaxx.fun` channel identity

### Phase G — Governance, legal, justice, and civic interfaces

Deliver:

- Governance
- MiResolve
- MiLegal
- MiJustice
- Redress
- Inside
- Campaign
- MiElection
- MiPublic Office
- Presidency profile
- Campaign-to-office transition controls

### Phase H — Jacksonville pilot backend

Deliver:

- Duval/Jacksonville place cell
- Local service registry
- Pilot data spaces
- Support and safety operations
- Community and cooperative profiles
- Offline test
- Export test
- Dispute routing test
- Financial reconciliation test
- Campaign and public-office separation test
- Recovery exercise

## 7. Backend production gate

The backend is not production-ready until all of these pass:

- Fresh install from pinned dependencies
- Reproducible database migration
- Restore from encrypted backup
- Authentication recovery
- RLS isolation tests
- OpenFGA authorization tests
- Capability revocation tests
- Idempotency tests
- Ledger invariant and concurrency tests
- Outbox replay tests
- Offline/reconnect tests
- Data export tests
- Deletion and legal-hold tests
- Abuse and rate-limit tests
- Secret-rotation test
- Dependency vulnerability scan
- API contract tests
- Accessibility-ready response metadata
- Observability and alert tests
- Manual human approval tests
- MiResolve/MiLegal/MiJustice routing tests
- Campaign-to-office transition test
- Shutdown and fork test

A green homepage or a successful login is not production readiness.

## 8. What will not be used as a shortcut

- No Firebase-only architecture
- No hidden proprietary hosted dependency
- No auto-generated API treated as the whole backend
- No single giant database table for all OSes
- No parallel money ledger
- No AI agent with unrestricted service-role access
- No production deployment of local development defaults
- No unverified “free hosting” promise
- No fake compliance claim
- No unreviewed third-party financial, health, legal, or election authority
- No placeholder endpoints presented as complete features

## 9. Frontend handoff contract

The frontend begins only after the backend exposes stable contracts for:

- Identity and session
- Cell and context selection
- Permissions and approvals
- Receipts and activity
- Data spaces
- OS discovery
- Support and disputes
- Knowledge and media
- Campaign website integration
- Money statements
- Offline status
- Export and deletion

The future frontend will use the `milyfe.fun` light-theme brand system, but branding must not be embedded into backend authority or data rules.

## 10. Final decision

The backend should begin with a **self-hosted Supabase/PostgreSQL foundation, a custom modular MiLyfe API, OpenFGA authorization, a PostgreSQL outbox, and explicit Kernel/MiData/MiMoney contracts**.

Appwrite, Keycloak, Temporal, NATS, Fineract, Mojaloop, ERPNext, PeerTube, and additional infrastructure remain carefully bounded options. They are not all installed at once, and none is allowed to silently become the authority for MiLyfe.
