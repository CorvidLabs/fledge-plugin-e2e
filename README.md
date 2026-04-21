# fledge-plugin-e2e

End-to-end test plugin for [fledge](https://github.com/CorvidLabs/fledge) — exercises every command and reports pass/fail status.

## Install

```bash
fledge plugin install CorvidLabs/fledge-plugin-e2e
```

## Usage

```bash
fledge e2e
```

Runs from the root of any git repo with a GitHub remote. The test harness:

- Scaffolds a temporary project to test `init`, `spec`, `run`, and `flow` commands
- Tests non-destructive commands against the current repo (issues, prs, checks, changelog, metrics, deps)
- Skips destructive operations (work start/pr/finish, publish, plugin install/remove)
- Skips AI-powered commands unless `ANTHROPIC_API_KEY` or `OPENAI_API_KEY` is set

### Environment variables

| Variable | Default | Description |
|----------|---------|-------------|
| `FLEDGE_BIN` | `fledge` | Path to the fledge binary |
| `E2E_TEMPLATE` | `rust-cli` | Template to use for init tests |
| `ANTHROPIC_API_KEY` | — | Enables AI command tests (review, ask) |
| `OPENAI_API_KEY` | — | Alternative AI key |

### Output

Prints a formatted report with pass/fail/skip counts and per-test timing:

```
╔══════════════════════════════════════════════════════════════╗
║                    fledge e2e test report                   ║
╠══════════════════════════════════════════════════════════════╣
║  Total: 44 tests  |  12s elapsed                           ║
║  Pass: 36  |  Fail: 0  |  Skip: 8                          ║
╠══════════════════════════════════════════════════════════════╣
║  ...                                                        ║
╚══════════════════════════════════════════════════════════════╝
```

Exits with code 1 if any tests fail.

## License

MIT
