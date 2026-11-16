# Issue

**Title:** Aggregate genes using the same method as cells

## Description

The current method to aggregate genes is very slow, especially when there are many small groups. For example, when I am pseudobulking modules but not TFs, each TF becomes it own "gene group." I don't see a reason why it can't be done using`my.aggregate.Matrix` like what is done for aggregating cells. I constructed a pseudobulk using both methods and the resulting matrices are equal to a tolerance of < 1e-15.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de92e4eb544c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.