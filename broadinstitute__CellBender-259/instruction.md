# Issue

**Title:** Fix posterior and estimator integer overflow bugs on Windows

## Description

The data structure used to store the full posterior is a `[m, c]` matrix, where `m` is n_barcodes times n_genes.  So `m` can be absolutely massive.

When `m` > maximum possible int32:

- the code behaved fine on Linux and Mac
- the code broke on Windows, leading to #252 

Including explicit casts to `uint64` seems to solve the problem on Windows (pending input on #252 ).

I have included a test which I believe might fail on Windows without this fix, though I do not have a Windows setup to test on yet.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `02dd763fdb3b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.