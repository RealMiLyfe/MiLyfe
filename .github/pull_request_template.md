# Pull Request Template

## Task Information
- **Issue ID**: [ISSUE-ID]
- **Objective**: [Brief description of what this PR accomplishes]
- **Branch**: [branch-name]
- **Agent Role**: [role - e.g., build agent, security agent, etc.]

## Summary of Changes
[Provide a clear, concise description of the changes made in this pull request.]

## Related Issues
- Fixes #[ISSUE-ID]
- Related to #[RELATED-ISSUE-ID] (if applicable)

## Architecture Impact
- [ ] No architecture changes
- [ ] Minor architecture changes (describe below)
- [ ] Major architecture changes (requires ADR)

If architecture changes were made:
- [ ] ADR created: [ADR-ID]
- [ ] ADR updated: [ADR-ID]
- [ ] No ADR required (explain why)

## Contract Impact
- [ ] No contract changes
- [ ] Contracts updated: [list contracts]
- [ ] New contracts created: [list contracts]
- [ ] Contract deletions: [list contracts]

## Security and Privacy Impact
- [ ] No security or privacy impact
- [ ] Security review required
- [ ] Privacy review required
- [ ] Security checks passed: [list checks]
- [ ] Privacy considerations: [describe]

## Testing
- [ ] Unit tests: [pass/fail/not run]
- [ ] Integration tests: [pass/fail/not run]
- [ ] Contract tests: [pass/fail/not run]
- [ ] Security scans: [pass/fail/not run]
- [ ] Accessibility tests: [pass/fail/not run]
- [ ] Other tests: [describe]

## Checklist
- [ ] I have read the root `AGENTS.md`
- [ ] I have read `docs/agent/STEERING-INDEX.md`
- [ ] I have read `docs/agent/CURRENT-STATE.md`
- [ ] I have read `docs/agent/ACTIVE-RISKS.md`
- [ ] I have read the assigned GitHub Issue in full
- [ ] I have confirmed the issue is not already claimed by another agent
- [ ] I have written an orientation comment on the issue before beginning work
- [ ] I have implemented only the approved task
- [ ] I have run all required tests and checks
- [ ] I have updated documentation as needed
- [ ] I have completed the handoff template
- [ ] I have requested the appropriate reviews
- [ ] I have not added unrelated refactors
- [ ] I have not added unnecessary dependencies
- [ ] I have not added secrets or real private data
- [ ] I have not bypassed permissions
- [ ] I have not made the browser or agent authoritative for money or identity
- [ ] I have not created placeholder behavior and called it complete
- [ ] I have not hid unsupported legal, financial, health, election, or psychological claims

## Screenshots or Evidence (where relevant)
[Add screenshots, videos, or other evidence demonstrating the changes work correctly.]

## Rollback Plan
[Describe how to rollback the changes if needed.]

## Migration Plan
[Describe any migration steps needed for existing data or systems.]

## Open Questions
- [List any open questions or uncertainties]

## Next Agent Handoff
- [Describe the exact next action for the next agent]

## Human Approval Required
- [ ] None
- [ ] Identity-related changes
- [ ] Permission changes
- [ ] $MLY ledger or settlement changes
- [ ] USD-facing rails changes
- [ ] Treasury or rewards changes
- [ ] Health or care authority changes
- [ ] Children or vulnerable people changes
- [ ] Campaigns or elections changes
- [ ] Public-office authority changes
- [ ] Legal or justice workflow changes
- [ ] Physical device actions
- [ ] MiPsyche continuity or identity changes
- [ ] Agent tool authority changes
- [ ] Security controls changes
- [ ] Public claims of readiness or legality