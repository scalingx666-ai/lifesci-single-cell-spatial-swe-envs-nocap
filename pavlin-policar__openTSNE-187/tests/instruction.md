# Issue

**Title:** Fix crash when dealing with super large affinity matrices

## Description

##### Issue
When an affinity matrix is super large, the `.indptr` becomes `np.int64`. The code handles only `np.int32`.


##### Description of changes
Handle both cases.


##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `970a8d5d3954`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.