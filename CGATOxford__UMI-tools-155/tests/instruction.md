# Issue

**Title:** {is} cell clustere refactor

## Description

Moves the cell cluster functor to the end of the module so that merging in other functionality will not be disrupted.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8193b9352f81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.