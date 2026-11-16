# Issue

**Title:** fix(estimators): accept an AnnData without X

## Description

## Summary
Estimators build their shadow AnnData with `adata.X.dtype`, so `GPCCA(kernel)` raised `AttributeError: 'NoneType' object has no attribute 'dtype'` when `adata.X` is `None`, as in an AnnData that holds only `obs`, `obsm` and graphs (e.g. a precomputed transition matrix on a large dataset). The shadow AnnData now has no `X` either.

## Testing
- New `TestGPCCASerialization::test_adata_without_x`: fits GPCCA through fate probabilities on an AnnData without `X` and checks `to_adata()`; it fails on `main` with the error above.
- `tests/test_gpcca.py -k "Serialization or test_compute_macrostates or fate"`: 38 passed, 1 xfailed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01CEkHnYavwEf7n32j7rNkPv

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0938e9ef795f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.