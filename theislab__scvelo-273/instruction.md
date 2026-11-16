# Issue

**Title:** Fix and refactor / Neighbors

## Description

## Changes

* Add the used representation to calculate the neighbor graph to `adata.uns["neighbors"]["params"]` in the function `neighbors`.

* Refactor the function `get_n_neighs` into a more concise and pythonic way.

## Related issues:
. .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b31dc47a100`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.