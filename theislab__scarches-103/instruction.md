# Issue

**Title:** Efficient stratifier_weights

## Description

stratifier_weights is currently a bottleneck when calling `.train()` in TRVAE (a dataset with ~1M cells will take ~10 min at this step). Profiling shows this is due to repeated use of `np.count_zero` on large vectors. This PR replaces `np.count_zero` with Counter and simplifies weight calculation. This step now takes ~30 seconds for ~1M cells.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f373a100e54`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.