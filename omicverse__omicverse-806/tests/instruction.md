# Issue

**Title:** feat(pp): out-of-core AnnDataOOM support across the ov.pp surface

## Description

## What

Makes the remaining `ov.pp` functions run **fully out-of-core** on an [`AnnDataOOM`](https://github.com/omicverse/anndata-oom) backend, under the same function names — peak RAM bounded by chunk size, not cell count. On the `is_oom(adata)` path each entry point dispatches to a chunked building block in `anndataoom`; the in-memory path is untouched.

| Function | OOM behaviour | verified (ts_5k) |
|---|---|---|
| `filter_cells` / `filter_genes` | chunked stat pass + lazy subset | ~35 MB, X stays backed |
| `highly_variable_genes` (seurat/cell_ranger/pearson) | chunked dispersion / Pearson | seurat 100% overlap vs scanpy |
| `normalize_total` + `log1p` | lazy `TransformedBackedArray` | allclose 2.4e-7 (was +227 MB materialise) |
| `highly_variable_features` (pegasus) | chunked mean/var + LOESS | 2000 HVF, X stays lazy |
| `normalize_pearson_residuals` | lazy `PearsonResidualBackedArray` | 3.8e-6 vs scanpy (was `NotImplementedError`) |
| `regress` | lazy `RegressedBackedArray`, one chunked OLS pass | honours custom `keys`; ~6e-7 vs sklearn |
| `scrublet` | bounded to the HVG subset (chunked prep) | ρ=0.98 vs in-memory (was full `to_memory()`) |

Unsupported sub-cases (e.g. `layer=`/`inplace=False` on the lazy paths, batch-aware pegasus) raise explicit `NotImplementedError` — no silent full-matrix materialisation.

## Compatibility / safety
- Branch is rebased on the latest `master` (**0 behind**), so it preserves all recent work including #798/#799 custom-keys `regress` — the OOM `regress` branch reuses the resolved+validated `keys`, not a hardcoded list.
- Requires `anndataoom` only on the OOM path (imported lazily inside the branches); omicverse imports cleanly without it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c830ad2fb60`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.