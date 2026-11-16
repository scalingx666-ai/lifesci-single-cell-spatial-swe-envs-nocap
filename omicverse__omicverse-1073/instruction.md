# Issue

**Title:** space: add CMAP, a third single-cell-to-spatial mapping method

## Description

Adds `ov.space.CMAP`, a third way to place single cells at spatial
coordinates, alongside `space.CellMap` (SpatRio, optimal transport) and
`space.Tangram`.

CMAP works in three levels: an SVM assigns each cell to a spatial domain, an
optimiser assigns it to a spot inside that domain, and interpolation over
neighbouring spots produces a coordinate.

```python
svg_list = ov.space.svg(adata_st, mode='prost', n_svgs=3000)
adata_sc, cell_spot_map = ov.space.CMAP(adata_sc, adata_st, spatial_genes=svg_list)
adata_sc.obsm['spatial_CMAP']      # (n_cells, 2)
```

## What this is a wrapper over

[`pycmap`](https://github.com/omicverse/py-CMAP) — the pure-Python port of R
CMAP ([SuoLab-GZLab/CMAP](https://github.com/SuoLab-GZLab/CMAP), MIT © 2025
KE Jincan). It is imported **lazily**, so omicverse gains no hard dependency
and a missing install produces a pip line rather than a traceback.

## How it differs from the two existing methods

CMAP needs the spatial object to already carry **spatial domain labels**
(`adata_st.obs['HMRF_cluster']` by default). CellMap and Tangram do not. The
wrapper checks for that key and for `obsm['spatial']` up front and raises
naming the three ways to produce them — `ov.space.clusters`, STAGATE, or
`pycmap.run_hmrf` for the original package's HMRF route — rather than failing
somewhere inside the port.

## Contract

All nine `register_function` fields are declared.

`requires` and `produces` use only the registry's own state keys. `_registry.py`
restricts them to `{layers, obsm, obsp, uns, var, obs, varm}`, so this
two-object function declares the **union** and says in the docstring which
object each key belongs to — the same thing `space.CellMap` does. (An earlier
draft of this patch used `obs_st`/`obsm_st` to mark the distinction; those are
not valid keys and the contract would have been malformed.)

| | |
|---|---|
| requires | `obs: [HMRF_cluster]`, `obsm: [spatial]` — both on `adata_st` |
| produces | `obs: [CMAP_domain, CMAP_svm_prob, CMAP_spot, CMAP_spot_prob, CMAP_entropy, CMAP_norm_entropy, CMAP_quality]`, `obsm: [spatial_CMAP]` — on `adata_sc` |

## One thing the docstring says explicitly

Numerical agreement with the R reference has **not** been measured. py-CMAP
records `parity.status: unverified`, and the docstring says results should be
read as the Python implementation's rather than as reproducing R exactly. That
will change when the parity gate is run against the R reference, which is
archived at the version used.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c89d5a8ea89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.