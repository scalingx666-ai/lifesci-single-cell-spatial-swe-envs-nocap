# Issue

**Title:** PHATE v0.4.0

## Description

Changeset:
* move `io`, `preprocessing`, and `plot` to `scprep`
* update handling of knn to fit `graphtools` v1.0.0.
* rename `k` to `knn` and `a` to `decay`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd8db69b1659`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.