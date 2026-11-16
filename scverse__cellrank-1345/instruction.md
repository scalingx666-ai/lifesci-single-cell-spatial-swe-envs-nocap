# Issue

**Title:** Explain why the coarse stationary distribution is missing in GPCCA

## Description

## What

Improves the diagnostics around the missing coarse-grained stationary distribution in `GPCCA`, without changing behavior.

- **Warn early** at `compute_macrostates` time: as soon as pygpcca returns no stationary probability, a warning explains why it happened and that automatic initial state prediction won't be available.
- **Explain the failure** in `predict_initial_states`: the bare `RuntimeError("No coarse-grained stationary distribution found.")` is replaced with a message that states the root cause and points to `set_initial_states()` as the manual alternative.

## Why

`predict_initial_states` relies on `coarse_stationary_distribution`, which pygpcca sets to `None` whenever the **microstate** stationary distribution of the transition matrix cannot be computed (the solve is wrapped in a `try/except` upstream that warns and returns `None`). This becomes fragile/infeasible on very large or (nearly) reducible transition matrices — exactly the case reported in , where the failure correlated with dataset size (million-cell runs).

Previously this only surfaced as a bare `RuntimeError` with no explanation. The workaround suggested in that issue thread — passing `predict_initial_states(n_states=...)` — does **not** actually bypass the failing path: the code only skips the stationary distribution when there is exactly one macrostate (`probs.shape[1] == 1`), which is why multiple users reported it didn't help.

## Notes for reviewers

- **No silent fallback.** Initial state prediction deliberately depends on the coarse stationary distribution, so the failure still raises. This PR only makes *why* it failed and *what to do next* clear.
- The two messages are consistent and both steer users to `set_initial_states()`.
- Pure messaging/logging change; no public API or behavior change.

Addresses .

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60c59c332a9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.