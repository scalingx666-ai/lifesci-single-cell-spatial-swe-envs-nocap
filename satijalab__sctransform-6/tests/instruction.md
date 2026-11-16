# Issue

**Title:** swap in future framework for mclapply

## Description

Replaces all occurrences of `mclapply` with `future_lapply`. 

No significant timing differences on the small test cases I ran. 

Note: the test suite will not currently pass, though the errors/warnings existed before this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b74b82d761b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.