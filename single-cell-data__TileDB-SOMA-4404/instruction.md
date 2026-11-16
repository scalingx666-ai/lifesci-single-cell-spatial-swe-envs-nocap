# Issue

**Title:** [python] Add missing bool column to remote test fixture

## Description

**Issue and/or context:** [SOMA-857] The remote test `test_experiment_axis_query` was failing because it filters on `is_b_cell`, a column that does not exist in the `small_pbmc` anndata created by the fixture.

**Changes:**

- Update the `small_pbmc()` test fixture to include the missing `is_b_cell` column.

**Notes for Reviewer:**

- I verified all local and remote tests pass on my local machine.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `817e7861b5b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.