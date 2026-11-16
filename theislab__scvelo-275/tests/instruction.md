# Issue

**Title:** Feat / Remove np.where wherever possible

## Description

## Changes

* `np.where` is replaced by the pandas index method `get_loc` wherever possible.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b31dc47a100`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.