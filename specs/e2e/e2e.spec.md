---
module: e2e
version: 2
status: active
files:
  - fledge-e2e

db_tables: []
depends_on: []
---

# E2e

## Purpose

Exercise fledge commands end to end from a real Git repository, scaffold disposable projects for mutating local tests, skip unavailable or externally destructive surfaces, and report timed pass/fail/skip results.

## Public API

| Category | Behavior |
|----------|----------|
| Disposable project | Scaffold a temporary template and exercise spec, task, and lane commands locally. |
| Current repository | Exercise non-destructive repository, changelog, metrics, dependency, and GitHub reads. |
| Optional plugins | Skip commands whose plugin is not installed rather than reporting false failures. |
| AI commands | Run only when an approved provider API key is present. |
| Report | Print per-test timing and aggregate pass, fail, and skip counts; fail if any test failed. |

## Invariants

1. Work, release, plugin installation/removal, pushes, and other destructive operations are never executed by the harness.
2. Project mutations occur only inside a temporary scaffold that is cleaned after the run.
3. Missing optional plugins and absent AI credentials produce SKIP, not PASS or FAIL.
4. The current repository must be a Git repository with a GitHub remote before hosted read tests run.
5. Any failed test yields a final non-zero exit status.
6. `FLEDGE_BIN` and `E2E_TEMPLATE` overrides are honored.

## Behavioral Examples

```
Given no AI credential and no optional metrics plugin
When the harness runs
Then AI and metrics cases are reported as skipped while core local cases still execute
```

## Error Cases

| Error | When | Behavior |
|-------|------|----------|
| Fledge unavailable | Configured binary cannot execute | Report failure and exit non-zero. |
| Unsupported repository | Current directory lacks required Git/GitHub context | Report the precondition failure. |
| Optional plugin absent | A plugin-provided command is unavailable | Mark its tests skipped. |
| Command regression | An expected non-destructive command returns unexpected status/output | Record failure and continue to the final report. |
| Temporary scaffold failure | Template or local project setup fails | Record affected cases as failed and clean available state. |

## Dependencies

- Bash and standard POSIX/Git tooling
- fledge CLI and optional fledge plugins
- GitHub connectivity for hosted read-only cases
- optional approved AI provider credentials

## Change Log

| Version | Date | Changes |
|---------|------|---------|
| 1 | 2026-07-12 | Document existing safe E2E harness behavior for SpecSync 5 adoption. |
| 2 | 2026-07-13 | Reconciled existing safety documentation and stable requirement IDs for SpecSync 5.0.1 governance; runtime behavior and independently authorized external E2E execution are unchanged. |
| 2026-07-13 | CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-e2e-fledge-plugin: Adopt SpecSync 5.0.1 and Trust 1.0.0 governance for the E2E Fledge plugin |
