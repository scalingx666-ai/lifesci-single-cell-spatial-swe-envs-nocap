# Issue

**Title:** fix(pca): OOM PCA — pass use_highly_variable to anndataoom instead of subset-wrap

## Description

## Summary

When ``ov.pp.pca`` runs against an ``AnnDataOOM``, we previously did:

```python
adata_comp = adata[:, mask_var] if mask_var is not None else adata
# ...
chunked_pca(adata_comp, layer="scaled", ...)
```

That ``adata[:, mask_var]`` wraps the ``ScaledBackedArray`` in a ``_SubsetBackedArray``. anndataoom's PCA fast-paths use ``isinstance(X, ScaledBackedArray)`` to dispatch — the subset wrap **fails the check** and falls through to the slow legacy chunked Halko. Worse: every chunked read of the subset wrap still materialises a full-width ``(chunk_size × n_vars_full)`` dense chunk and slices columns only at the very end. On a 232 k × 58 k matrix that's 96 % wasted work per chunk × 10 PCA passes.

## Fix

Pass the original ``adata`` (not the subset view) to ``chunked_pca`` and forward ``use_highly_variable=True`` (when ``mask_var`` is resolved). anndataoom 0.1.6 adds the kwarg and resolves the HVG index from ``adata.var['highly_variable_features']`` (or ``'highly_variable'``) internally, slicing columns INSIDE each fast path:

- Path 1 (auto-materialise) builds only the HVG columns → 232 k × **2 000** = 1.86 GB, easily fits the 16 GB threshold (was: 54 GB, too big).
- Path 2 (implicit centering) slices each sparse log-norm chunk to HVG columns before the matvec.
- Path 3 (legacy fallback) inherits the same slicing.

The variance / loadings post-processing reads the effective ``n_vars`` from ``components.shape[1]`` (= n_HVGs when use_hvg, else full ``n_vars``).

## Measured

End-to-end on real TS-Vasculature (42 k cells × 60 606 genes, HVG=2 000) on a CPU node through ``ov.pp.pca``:

|  | PCA stage |
|---|---|
| Before this PR | **370.6 s** |
| After this PR + anndataoom 0.1.6 | **39.6 s** |
| **Speedup** | **9.4 ×** |

## Requires

-  — adds ``use_highly_variable`` to ``chunked_pca``. Lands as anndataoom 0.1.6.

This PR is a no-op without the anndataoom side (it gracefully passes a kwarg older versions ignore via ``**kwargs``… actually no, older anndataoom will raise ``TypeError`` on the unknown kwarg). Bump the install constraint when merging.

## Test plan

- [x] End-to-end: ``ov.pp.qc → preprocess → scale → pca`` on TS-Vasculature, observe PCA stage drops from 370 s → 39 s.
- [x] Output shape: ``adata.obsm['X_pca']`` is ``(42577, 50)`` (matches v0.1.5 shape exactly).
- [ ] CI: existing test suite (no direct test added here — the meaningful regression coverage is upstream in anndataoom).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a295c0a67a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.