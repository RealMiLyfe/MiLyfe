# Dependency Update Policy

This file defines the policy for automated dependency updates using Dependabot or Renovate.

## Update Frequency
- **Daily**: Security updates for direct dependencies
- **Weekly**: Minor and patch updates for direct dependencies
- **Monthly**: Major updates for direct dependencies (requires manual review)
- **Quarterly**: Updates for indirect dependencies

## Automation Rules
- Automatically create pull requests for:
  - Dependency version updates
  - Security updates
  - Patch updates within the same minor version
- Do not automatically merge - all updates require review
- Label dependency update PRs with `dependencies` and `automated-update`

## Package Rules
- Pin versions for critical security packages
- Allow automatic updates for non-breaking changes
- Require manual review for major version updates of core frameworks
- Exclude development dependencies from automatic updates unless they affect security

## Review Requirements
- All dependency updates must pass CI before merging
- Security updates get priority review
- Major version updates require architecture review
- Updates to contracts or security-related packages require security review

## Exclusions
- Do not automatically update:
  - Compiler versions without explicit testing
  - Database migration tools without backup verification
  - Authentication libraries without security review
  - Contract code generators without verification