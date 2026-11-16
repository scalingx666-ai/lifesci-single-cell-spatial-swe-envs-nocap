# Issue

**Title:** [r] remove error from `cbind` and `rbind`, when matrices are of different types, to upcast instead of erroring out.

## Description

Change the error when using `cbind()` and `rbind()` to stop erroring out when the provided matrices are of different types.  Instead, spit out a warning, and upcast instead.  
Also provided a small test all permutations of matrix types for two matrices will still function as expected.

Addresses #261

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2026c3509f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.