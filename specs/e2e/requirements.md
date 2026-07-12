---
spec: e2e.spec.md
---

## User Stories

- As a fledge maintainer, I want a broad end-to-end regression report without destructive repository operations.

## Acceptance Criteria

### REQ-e2e-001

The harness SHALL exercise core commands using a disposable scaffold and non-destructive reads against the current GitHub repository.

### REQ-e2e-002

The harness SHALL skip unavailable plugin and AI commands with an explicit reason.

### REQ-e2e-003

The harness SHALL never perform work commits, pushes, releases, or plugin installation/removal.

### REQ-e2e-004

The report SHALL include per-test timing and aggregate pass, fail, and skip counts and exit non-zero when failures exist.

## Constraints

- Full execution requires fledge, Git/GitHub context, network access, and optionally installed plugins or AI credentials.

## Out of Scope

- Destructive workflows and unapproved external writes.
