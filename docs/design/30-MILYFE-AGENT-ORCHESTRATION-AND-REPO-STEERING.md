# MiLyfe Agent Orchestration and Repository Steering Design

**Status:** Design authority
**Purpose:** Coordinate multiple Arena AI Agent Mode sessions and human contributors working on one new MiLyfe GitHub repository without conflicting branches, duplicated decisions, unsafe changes, leaked secrets, or unclear handoffs.
**Mode:** Repository governance and agent workflow design; no product implementation code

## 1. Core operating rule

No agent is allowed to treat the repository as an empty canvas.

Every agent must first read the current steering files, current state, assigned issue, relevant contracts, and active decisions. Every agent must leave a clear handoff for the next agent.

The repository is a coordinated system, not a collection of independent chat sessions.

## 2. Source-of-truth hierarchy

When documents conflict, agents use this order:

1. Human-approved repository constitution
2. Root `AGENTS.md`
3. Security and safety policies
4. Approved architecture decision records
5. Versioned contracts and schemas
6. Current roadmap and release gate
7. Domain-level `AGENTS.md`
8. GitHub issue and approved task specification
9. Pull-request discussion
10. Agent assumptions

An agent may not resolve a conflict by silently choosing its preferred interpretation. It must report the conflict and request an architecture decision.

A lower-level steering file may clarify or strengthen a higher-level rule. It may not weaken or replace a higher-level invariant.

## 3. Canonical repository structure

The new repository should contain this steering and coordination structure:

```text
AGENTS.md
README.md
CONTRIBUTING.md
CODE_OF_CONDUCT.md
SECURITY.md
LICENSE
NOTICE

/.github/
  CODEOWNERS
  pull_request_template.md
  issue_template/
  workflows/
  dependabot-or-renovate-policy.md

/.agents/
  README.md
  roles/
  skills/
  prompts/

/docs/
  /constitution/
  /architecture/
  /decisions/
  /contracts/
  /roadmap/
  /security/
  /legal/
  /brand/
  /operations/
  /agent/
    STEERING-INDEX.md
    CURRENT-STATE.md
    WORK-QUEUE.md
    ACTIVE-RISKS.md
    HANDOFF-TEMPLATE.md
    RELEASE-READINESS.md
  /os/
    /kernel/
    /onboard/
    /psyche/
    /agent/
    /market/
    /forge/
    /money/
    /scale/
    /device/
    /security/
    /dev/

/adr/
  ADR-0001-template.md

/contracts/
  /api/
  /events/
  /receipts/
  /permissions/
  /data/

/tests/
  /contract/
  /security/
  /integration/
  /property/
  /e2e/
  /accessibility/
  /offline/

/ops/
  /runbooks/
  /backups/
  /incidents/
  /release/
```

The final implementation repository may adapt the exact folder layout, but the steering, state, contract, decision, security, and handoff functions are mandatory.

## 4. Required steering files

### 4.1 Root `AGENTS.md`

The root file contains only rules that apply to every agent and contributor:

- MiLyfe naming and brand law
- Mission and non-negotiable invariants
- Source-of-truth hierarchy
- No direct pushes to protected branches
- One issue and one branch per task
- No secrets or private data
- No fake endpoints, fake balances, fake receipts, or placeholder completion claims
- No silent architecture decisions
- High-impact change restrictions
- Required tests and handoff
- Stop conditions
- Security and publication rules

The root file should remain short enough to read before every task.

### 4.2 `STEERING-INDEX.md`

Lists every steering file, its scope, owner, authority, and update rule.

### 4.3 `CURRENT-STATE.md`

The single short current-state snapshot:

- Current release or wave
- Last merged work
- Active blockers
- Active risks
- Next approved tasks
- Pending decisions
- Required human approvals
- Last updated commit
- Last updated date

Only the integration/release agent updates the canonical current-state file through a pull request.

### 4.4 `WORK-QUEUE.md`

Lists work by state:

- Proposed
- Ready
- Claimed
- In progress
- Blocked
- In review
- Approved
- Merged
- Deferred
- Cancelled

GitHub Issues remain the live task authority. The repository queue is a synchronized summary, not a competing task tracker.

### 4.5 `ACTIVE-RISKS.md`

Tracks:

- Risk
- Severity
- Affected OS
- Owner
- Mitigation
- Trigger
- Status
- Review date
- Required decision

### 4.6 `HANDOFF-TEMPLATE.md`

Every agent completes a handoff before ending a task.

Required fields:

- Task ID
- Branch
- Agent role
- Objective
- Work completed
- Files changed
- Tests run
- Security checks run
- Decisions made
- Assumptions
- Open questions
- Blockers
- Migration or rollback concerns
- Next recommended action
- Human approval required

## 5. Repository authority roles

### Human product steward

Owns product intent, final scope, and high-impact decisions.

### Orchestrator agent

Breaks approved roadmap work into tasks, checks dependencies, assigns work, and prevents duplicate effort.

### Architecture agent

Maintains architecture, contracts, ADRs, and boundaries. It does not silently implement disputed design.

### Build agent

Implements one approved task on one branch.

### Security agent

Reviews threats, secrets, permissions, dependencies, release risk, and security evidence.

### Test and quality agent

Runs contract, integration, property, browser, accessibility, offline, and regression testing.

### Documentation agent

Maintains user, developer, legal, operational, and release documentation.

### Release/integration agent

Checks the complete PR, resolves integration order, updates current state, and prepares release evidence.

### Human approver

Approves high-impact changes involving identity, money, legal, health, children, campaigns, public office, device action, agent authority, security, or MiPsyche continuity.

No single AI agent may act as architecture owner, implementer, security approver, and release approver for a high-impact change.

## 6. Branch protocol

### Protected branches

- `main` — production-quality source of truth; protected
- Optional `pilot` — controlled pilot release line; protected
- No permanent agent-owned development branch

Avoid a long-lived `develop` branch unless the release agent documents why it is necessary. Short-lived branches reduce drift and conflicts.

### Branch names

```text
agent/MLY-####/short-task-name
human/MLY-####/short-task-name
security/MLY-####/short-task-name
architecture/MLY-####/short-task-name
docs/MLY-####/short-task-name
hotfix/MLY-####/short-task-name
revert/MLY-####/short-task-name
```

One issue equals one branch. One branch equals one coherent change.

### Branch rules

- Never commit directly to `main`.
- Never work on another agent’s branch without explicit handoff.
- Never reuse a completed branch for a new task.
- Rebase or merge from current `main` before requesting review.
- Keep branches short-lived.
- Do not mix unrelated OS changes in one branch.
- Do not resolve conflicts by deleting another agent’s work without review.
- Use a revert branch for reversals; preserve history.

## 7. GitHub repository protections

Before any implementation work begins, configure the new repository with:

- Protected `main` branch
- Pull request required for every merge
- No force-push to protected branches
- No branch deletion for protected branches
- Required status checks
- Required code-owner review
- Stale approval dismissal after relevant changes
- Signed-commit or signed-release policy
- Environment protection for pilot and production
- No production secrets in ordinary repository or agent contexts
- Separate development, pilot, and production environments
- Private security advisory intake
- Dependabot or Renovate review policy
- Secret scanning and push protection where available
- Issue templates
- Pull-request template
- CODEOWNERS
- Release permissions limited to approved maintainers
- Audit history retained

GitHub settings are infrastructure controls, not substitutes for MiSecurity OS. The repository must still be recoverable from the canonical source and public mirror policy.

## 8. Issue and task protocol

Every task begins as a GitHub Issue with:

- Task ID
- User or system outcome
- Scope
- Non-goals
- Relevant OS
- Dependencies
- Required contracts
- Security class
- Data class
- Acceptance criteria
- Test requirements
- Human approval requirements
- Rollback plan
- Owner
- Reviewer

Labels should include:

- `os:kernel`
- `os:onboard`
- `os:psyche`
- `os:agent`
- `os:market`
- `os:forge`
- `os:money`
- `os:scale`
- `os:device`
- `os:security`
- `os:dev`
- `type:feature`
- `type:bug`
- `type:docs`
- `type:contract`
- `type:security`
- `type:architecture`
- `risk:low`
- `risk:medium`
- `risk:high`
- `status:blocked`
- `status:needs-human`

An agent claims a task by commenting on the issue with its branch name and scope. If another agent has already claimed it, the second agent must not start duplicate work.

## 9. Agent session protocol

### At session start

The agent must:

1. Read root `AGENTS.md`.
2. Read `STEERING-INDEX.md`.
3. Read `CURRENT-STATE.md`.
4. Read active risks.
5. Read the assigned issue.
6. Read relevant architecture and contracts.
7. Inspect the current branch and working tree.
8. Check whether the issue is already claimed.
9. Identify required human approvals.
10. State its intended scope before changing files.

### During work

The agent must:

- Stay within the issue scope.
- Update the issue when blocked.
- Record architecture decisions as ADRs.
- Record contract changes in versioned contracts.
- Keep security and privacy boundaries visible.
- Use synthetic data in tests.
- Run required checks before review.
- Avoid unrelated cleanup.
- Stop when a high-impact decision is unresolved.

### At session end

The agent must:

1. Run status and diff review.
2. Run required tests.
3. Run security and secret scans.
4. Update documentation.
5. Complete the handoff file.
6. Comment on the issue with the status.
7. Open or update the pull request.
8. State blockers and next steps.
9. Leave the branch in a recoverable state.

## 10. Pull-request protocol

Every pull request includes:

- Task ID
- Problem solved
- Scope and non-scope
- Files changed
- Architecture impact
- Contract impact
- Data and privacy impact
- Security impact
- Money impact
- Agent/device impact
- Tests run
- Screenshots or evidence where relevant
- Migration plan
- Rollback plan
- Open questions
- Reviewer requests
- Human approval requirements

Required review paths:

- Architecture review for contract or boundary changes
- Security review for security, identity, permission, data, device, agent, or release changes
- Money review for ledger, settlement, reward, treasury, or marketplace-value changes
- Legal review for public claims, terms, campaigns, external financial rails, health, or public office
- MiPsyche review for continuity, memory, identity, personality, values, or digital-being status changes

## 11. Communication protocol between agents

Agents communicate through durable artifacts, not hidden chat assumptions.

### Issue comments

Used for live task status, blockers, and questions.

### Pull-request body

Used for change summary, evidence, risk, and review instructions.

### ADRs

Used for durable architecture decisions.

### Contracts

Used for API, event, receipt, data, permission, and versioned behavior.

### Handoff file

Used for the next agent to continue exactly where the previous agent stopped.

### Current state

Used by every new session to understand the merged repository state.

A chat conversation is never the only location for a consequential decision.

## 12. Conflict protocol

When agents disagree:

1. Stop implementation of the disputed behavior.
2. Record both interpretations.
3. Identify affected authority, contracts, users, and risks.
4. Create or update an ADR request.
5. Label the issue `status:needs-human` if it affects a reserved action.
6. Continue only with non-conflicting work.
7. Update the final decision in the repository.

No agent is rewarded for guessing through ambiguity.

## 13. High-impact stop conditions

The agent must stop and request human approval when a task changes:

- Identity or recovery
- Permissions
- `$MLY` ledger or settlement
- USD-facing rails
- Rewards or treasury
- Health or care authority
- Children or vulnerable people
- Campaigns or elections
- Public-office authority
- Legal or justice workflows
- Physical-device actions
- MiPsyche continuity or identity
- Agent tool authority
- Security controls
- Public claims of readiness or legality

## 14. Definition of clean collaboration

The repository is considered coordinated when:

- Every active task has one owner.
- Every branch maps to one issue.
- Every high-impact change has the right reviewer.
- Current state is accurate.
- No unresolved architecture conflict is hidden in code.
- No branch silently changes a contract.
- Every PR explains tests, security, privacy, and rollback.
- Agents can resume work from the repository without needing private chat history.
- A new agent can understand what happened in the previous session within one orientation pass.
