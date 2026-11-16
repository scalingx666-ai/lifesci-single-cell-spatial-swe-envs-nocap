# Issue

**Title:** Correctly handle non-finite numbers in heuristic determination of X distribution

## Description

The existing heuristic did not account for non-finites.  This PR:
* Adds explicit support to the algorithm for non-finites, plus a few other edge conditions (eg, sparse array in an  unsupported format)
* adds test cases for the above

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b1ab02a6011`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.