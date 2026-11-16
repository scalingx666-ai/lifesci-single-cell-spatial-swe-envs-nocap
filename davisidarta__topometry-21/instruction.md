# Issue

**Title:** refactor distance functions

## Description

## Summary
- streamline distance module to only include euclidean, poincaré, and cosine metrics
- add numba-accelerated implementations and parallel pairwise helpers
- expose parallel matrix distance helpers with optional `n_jobs`

## Testing
- `pytest`

------
https://chatgpt.com/codex/tasks/task_e_68bb70d76710832c9eb2373fb5006b8b

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d5ab4d30991`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.