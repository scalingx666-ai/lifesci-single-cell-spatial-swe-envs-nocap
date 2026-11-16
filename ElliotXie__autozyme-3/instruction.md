# Issue

**Title:** [seurat] fix SCTransform object bloat on qs2/saveRDS

## Description

## Problem

Community report: *"after using autozyme the object saved with qs2 becomes very large."* Reproduced — it is **SCTransform-specific**.

pbmc68k, 5,000-cell subsample, `SCTransform(obj)` defaults, `qs2::qs_save`:

| arm | qs2 file |
|---|---|
| baseline (no autozyme) | 112.66 MB |
| autozyme (bug) | **324.02 MB** (2.88x) |
| autozyme (this fix) | 112.18 MB |

`object.size` is ~identical for both arms (215 MB) — it does not recurse into closure environments, but `qs2`/`saveRDS` serialize them in full.

## Root cause

`SCTModel@arguments$row_gmean` = **212 MB on disk, 0.01 MB by object.size**. The turbo SCT path temporarily swaps `sctransform::row_gmean` for a `cached_row_gmean` closure whose env is the whole `fast_SCTransform` frame (full UMI matrix). `.seurat_sct_fast_vst` does `arguments <- as.list(environment())` and strips only `umi`/`cell_attr`, so the poisoned closure rides into `arguments`, which is persisted into `SCTModel@arguments`. Grows without bound in cell count. Standard Normalize→Scale→PCA→cluster pipeline is unaffected.

## Fix

Drop function-valued entries from `arguments` before persisting (upstream sctransform stores only scalar params there).

## Validation

- End-to-end: fixed file **112.18 MB**, 0 function args remain.
- **Numerically inert**: `scale.data` bit-identical to pre-fix (`all.equal == TRUE`).
- Speed preserved: SCT **4.05x**; filter runs once per call outside hot path (~8 µs).

## Follow-up (not in this PR)

Version bump + package rebuild needed for installed users.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5dcd64b0017`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.