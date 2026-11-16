# Issue

**Title:** Workaround for -1 in pynndescent index

## Description

.

Changes:

*    Query() is only used for k>15.
*    n_jobs fixed to 1 for sparse inputs to avoid a pynndescent bug
*    find all points where index contains -1 values, and let them randomly attract each other.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e3b93e75061`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.