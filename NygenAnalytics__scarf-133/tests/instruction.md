# Issue

**Title:** Update Mark HVGS

## Description

PR for updating `mark_hvgs()` in `assay.py`

Updates:
1. Separated summary statistics calculation from `mark_hvgs()`
2. Performed some type checking
3. Check for `lowess_frac` between 0 and 1

Notebook with multiple iterations of the functions `set_summary_stats()` and `mark_hvgs()` with different parameters to check if the function is working as expected is [here](https://github.com/Gautam8387/scarf-pr-exp/tree/main/03-mark-hvgs).

All tests pass

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31fe77208ba7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.