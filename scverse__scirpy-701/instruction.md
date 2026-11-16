# Issue

**Title:** Speed up identity distance metric computation for two  different sequence arrays

## Description

## Summary

This PR speeds up the identity distance metric computation when comparing _two different_ sequence arrays via the `IdentityDistanceCalculator`.

Instead of checking every pairwise combination of `seqs` and `seqs2`, the implementation now builds a lookup from sequences in `seqs2` to their column indices and uses it to get matching matrix entries directly.

For example, the previous performance issue became a problem when running the following call with a large number of cells:
```python
ir.pp.ir_dist(mdata, vdjdb, metric="identity", sequence="aa")
```

With this change, I was able to run the `IdentityDistanceCalculator` with millions of sequences in seconds.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `05344e54f3ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.