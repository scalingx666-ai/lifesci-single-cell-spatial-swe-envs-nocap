# Issue

**Title:** add rlang traceback in seurat methods

## Description

When seurat fails, it gives no traceback, e.g. [here](https://github.com/openproblems-bio/openproblems/actions/runs/3205713057/jobs/5281423215) (due to being run as an external process.) This fixes that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9317caeb1e7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.