# Issue

**Title:** Scope PrepareEnv pip checks to the requested dependency closure

## Description

## Summary
- Scope `PrepareEnv()` `pip check` failures to the requested module's transitive dependency closure: conflicts in that closure still hard-fail, while unrelated legacy conflicts become warnings with rebuild guidance.
- Pin compatible JAX companions for scVI (`jax`/`jaxlib` 0.4.38 with matching `numpyro`, `optax`, `flax`, and related packages), reject incompatible scVI/moscot mixes in one environment, and add the missing `jax==0.4.10` pin for Cell2fate.
- Retain original package-install error details and add unit tests covering closure-scoped conflict handling.

.

## Test plan
- [ ] CI R-CMD-check and key Suggests
- [ ] Confirm CellRank-only prepare no longer stops on leftover scVI/PHATE conflicts
- [ ] Confirm CellRank→pygpcca→jinja2 conflicts still hard-fail
- [ ] Confirm requesting both scVI and moscot in one env is rejected

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce3b500d73a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.