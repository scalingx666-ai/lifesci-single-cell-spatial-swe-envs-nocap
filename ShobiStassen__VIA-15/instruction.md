# Issue

**Title:** Refactoring of some functions

## Description

- Refactoring of `make_knn_struct`, `make_csrmatrix_noselfloop` and beginning of `run_subPARC` to reduce code duplication and number of lines of code.

- Added documentation (unmpy style) to male_knn_struct and `make_csrmatrix_noselfloop`

- Added a `distance_factor = 0.01` parameter to `make_csrmatrix_noselfloop` so it can be used either for clustergraph creation or random walk graph creation. (In the case of the cluster graph passing `distance_factor = 0.05`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c1b69ac2bc1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.