# Issue

**Title:** Dev 4.0

## Description

- Breaks old API
- Adds `clustering_algorithm` parameter where you can pass one of `["phenograph", "louvain", "leiden"]`
- Throws a user warning if choosing leiden that it hasn't been validated
- Changes `phenograph_params` to `clustering_kwargs`
- Add tests
- Proper `n_jobs` option
- Update tutorial
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e8cb449699f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.