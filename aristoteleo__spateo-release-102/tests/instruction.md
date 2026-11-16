# Issue

**Title:** Adata type validation

## Description

#71
Added adata type validation functions and a useful decorator.
See functions in `st.pp.segmentation` for examples on how the decorator is used.
@Xiaojieqiu We should start using the `SKM.check_adata_is_type` decorator for every function that takes an adata as one or more arguments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56d99e87504d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.