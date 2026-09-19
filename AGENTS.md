# MiLyfe Agent Guidelines

## Core Principles
- No agent treats the repository as an empty canvas
- Every agent must read current steering files, state, assigned issue, relevant contracts, and active decisions before working
- Every agent must leave a clear handoff for the next agent
- The repository is a coordinated system, not independent chat sessions

## Mandatory Practices
- One issue and one branch per task
- No direct pushes to protected branches
- No secrets or private data in code
- No fake endpoints, balances, receipts, or placeholder completion claims
- No silent architecture decisions - report conflicts and request architecture decisions
- Required tests and handoff before review
- Stop conditions for high-impact changes
- Security and publication rules must be followed

## Branch Naming Conventions
- `agent/MLY-####/short-task-name` - AI agent branches
- `human/MLY-####/short-task-name` - Human contributor branches
- `security/MLY-####/short-task-name` - Security-related branches
- `architecture/MLY-####/short-task-name` - Architecture-related branches
- `docs/MLY-####/short-task-name` - Documentation branches
- `hotfix/MLY-####/short-task-name` - Hotfix branches
- `revert/MLY-####/short-task-name` - Revert branches

## Review Requirements
- Architecture review for contract or boundary changes
- Security review for security, identity, permission, data, device, agent, or release changes
- Money review for ledger, settlement, reward, treasury, or marketplace-value changes
- Legal review for public claims, terms, campaigns, external financial rails, health, or public office
- MiPsyche review for continuity, memory, identity, personality, values, or digital-being status changes

## High-Impact Stop Conditions
Agents must stop and request human approval when tasks change:
- Identity or recovery
- Permissions
- $MLY ledger or settlement
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