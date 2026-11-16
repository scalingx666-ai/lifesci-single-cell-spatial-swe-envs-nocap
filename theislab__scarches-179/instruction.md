# Issue

**Title:** Have `_validate_var_names` support `csr_matrix`

## Description

When reference and query dataset have different `var_names`, and `adata.X` is a `scipy.sparse.csr_matrix`, then `_validate_var_names` fails with a `ValueError: zero-dimensional arrays cannot be concatenated`.
It might be nice to support sparse matrices as input, since it's often the default in AnnData.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e172d77f57cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.