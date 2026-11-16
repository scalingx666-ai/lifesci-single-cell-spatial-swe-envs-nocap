# Issue

**Title:** fix(rtk): recompute transition matrix when conn_weight changes

## Description

## Description

`RealTimeKernel.compute_transition_matrix` did not include `conn_weight` in the parameters used to detect cache reuse (`cache_params` only held `threshold` and `self_transitions`). As a result, changing **only** `conn_weight` on an existing kernel object silently returned the stale, already-computed transition matrix instead of recomputing it. `conn_weight` was also missing from `kernel.params`.

This adds `conn_weight` to `cache_params`, so a changed value triggers a recomputation and is correctly recorded in `params`. This matches the reporter's diagnosis in #1271 (manually setting `tmk._params["conn_weight"]` worked around it).

## Changes

- `src/cellrank/kernels/_real_time_kernel.py`: add `conn_weight` to `cache_params`.
- `tests/test_kernels.py`: add `test_recompute_on_changed_conn_weight`, a regression test using explicit couplings (no moscot/wot dependency) asserting the transition matrix changes when only `conn_weight` is altered, and that `params["conn_weight"]` is recorded.

## Testing

`TestRealTimeKernel` passes (8 passed, 5 skipped — moscot/wot/R not installed).

. Related to #1245.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e443e9c8f1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.