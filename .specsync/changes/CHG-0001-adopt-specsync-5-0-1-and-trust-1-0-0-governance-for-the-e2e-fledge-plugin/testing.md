---
change: CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-e2e-fledge-plugin
artifact: testing
---

# Testing

- `shellcheck fledge-e2e`
- `specsync check --strict --force` at advisory threshold 0
- `specsync agents status`
- `fledge trust doctor` and `fledge trust verify`
- Full `fledge e2e` remains independently controlled
