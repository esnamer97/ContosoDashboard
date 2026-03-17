<!--
Sync Impact Report
Version change: N/A → 1.0.0
Modified principles:
 - (none; first ratification)
Added sections:
 - Non-Functional Constraints
 - Development Workflow
Removed sections:
 - (none)
Templates reviewed:
 - ✅ .specify/templates/plan-template.md
 - ✅ .specify/templates/spec-template.md
 - ✅ .specify/templates/tasks-template.md
 - ✅ .specify/templates/constitution-template.md
 - ⚠ pending: none
Follow-up TODOs:
 - None
-->

# Contoso Dashboard Constitution

## Core Principles

### Value-First Delivery

The team MUST deliver small, usable increments that can be validated with real users. Each change is expected to provide observable value to at least one stakeholder and be deployable in isolation.

### Quality & Safety (Tested & Reliable)

All behavior MUST be covered by automated tests (unit, integration, or end‑to‑end) before it is accepted. The codebase MUST be protected by continuous integration that prevents regressions and enforces static checks (linting, formatting, type analysis).

### Inclusive & Accessible Experience

All user-facing interfaces MUST meet WCAG 2.1 AA accessibility guidelines and support the primary locales listed in the README. Accessibility issues are treated as functional defects.

### Secure & Privacy‑First

Security is non‑negotiable: authentication, authorization, data handling, and secrets MUST follow principle of least privilege. Sensitive data MUST be protected in transit and at rest, and privacy requirements MUST be documented for all data collection.

### Maintainable & Simple

Code and architecture MUST favor simplicity, readability, and maintainability. Avoid premature optimization and over-engineering; prefer clear intent over cleverness. Documentation and code comments MUST keep the system understandable for new contributors.

## Non-Functional Constraints

The project MUST operate reliably within the environments stated in `README.md` and `launchSettings.json`. Performance, reliability, and security constraints include:

- **Browser support**: Modern evergreen browsers (latest Chrome, Edge, Firefox, Safari) plus the latest stable version of Edge WebView2.
- **Performance**: UI interactions should be responsive (<= 200ms for key actions) and page loads should be practical for typical user scenarios.
- **Reliability**: All user-visible errors MUST be handled gracefully with clear recovery paths.
- **Compliance**: Follow applicable privacy and data handling laws (e.g., GDPR) when collecting or storing personal information.

## Development Workflow

- All changes MUST be made through pull requests (PRs) targeting the main branch.
- PRs MUST include:
  - A clear description of what changed and why.
  - Links to any related issues or specs.
  - A checklist mapping to the relevant constitution principles (e.g., "✅ Tests added", "✅ Security review done").
- Code review:
  - Every PR MUST be reviewed and approved by at least one peer before merging.
  - Reviewers MUST verify that changes align with the constitution and do not introduce technical debt without explicit justification.
- Versioning:
  - Tracks semantic versioning for releases; patch releases for fixes, minor for new backwards‑compatible features, major for breaking changes.
- CI:
  - CI must run on every PR and on `main`, catching build failures, lint errors, and test regressions.

## Governance

This constitution is the source of truth for development decisions in Contoso Dashboard. It supersedes informal practices and is referenced during planning, review, and implementation.

- **Amendments**:
  - Amendments require a PR with:
    - A summary of the change and the motivation.
    - A list of affected principles and any downstream impacts.
    - A version bump following the semantic rules in this section.
  - Amendments take effect once merged into `main`.
- **Versioning**:
  - Bumps follow semantic versioning:
    - **MAJOR** when principles are removed or redefined in a breaking way.
    - **MINOR** when new principles/sections are added or when guidance is materially expanded.
    - **PATCH** for clarifications, wording edits, typo fixes, or non‑semantic refinements.
- **Compliance**:
  - Every PR should include a brief statement of how the change aligns with constitution principles.
  - The team should periodically (at least once per quarter) review the constitution for relevance and applicability.

**Version**: 1.0.0 | **Ratified**: 2026-03-16 | **Last Amended**: 2026-03-16
