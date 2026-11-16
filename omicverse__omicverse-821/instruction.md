# Issue

**Title:** feat(pp): parametric UMAP returns a reusable model for projecting new data

## Description

Related to #809.

## What

`ov.pp.umap(adata, method='pumap')` now **returns the fitted parametric-UMAP model** instead of discarding it, so the learned mapping can be reused to place new cells onto the same embedding (the atlas / reference-mapping use case the requester described).

```python
model = ov.pp.umap(ref, method='pumap')   # fits + writes ref.obsm['X_umap']
new_embedding = model.transform(new_X)     # project NEW data through the same rule
model.save('ref_pumap.pkl')
model = ov.pp.load_pumap('ref_pumap.pkl')
```

- `method='pumap'` is now honoured in **any** `ov.settings.mode` (it's a deliberate atlas choice), not overridden by the mixed-mode non-parametric default.
- `ov.pp.load_pumap` re-exported for reloading saved models.
- Non-parametric backends keep their classic in-place/copy return; only `method='pumap'` returns a model.

## Tutorial

`examples/parametric_umap_projection.md` — fit on a reference → bring new data into the **same PCA space** → `model.transform` → plot; plus `save`/`load_pumap` and a backend-choice table (when to use `pumap` vs the default non-parametric UMAP).

## Tests

`tests/pp/test_pumap_model.py` (GPU-gated): model is returned, projects new data to `(n_query, 2)` deterministically, and survives a save/load round-trip. Passing locally on H100.

## Context (re: #809 default backend)

The other half of #809 — *don't make the parametric UMAP the mixed-mode default* — was already addressed in #812: `cpu-gpu-mixed` now defaults to a **non-parametric** GPU UMAP whose output matches scanpy. This PR keeps the parametric backend fully available and now properly reusable via `method='pumap'`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c083f478f78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.