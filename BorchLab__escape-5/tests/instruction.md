# Issue

**Title:** Fix all gene symbols being pulled from human list in getGeneSets.

## Description

Previous code always used the human gene symbols for msigdbr even if alternative species were used. This fixes that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `02d35b1e2335`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.