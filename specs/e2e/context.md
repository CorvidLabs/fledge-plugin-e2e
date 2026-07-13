---
spec: e2e.spec.md
---

## Context

This shell harness provides broad command-level confidence while deliberately isolating local mutations and avoiding repository state changes.

## Related Modules

- fledge CLI and official plugins

## Design Decisions

- Separate disposable local tests from current-repository read tests.
- Treat missing optional capabilities as explicit skips.
