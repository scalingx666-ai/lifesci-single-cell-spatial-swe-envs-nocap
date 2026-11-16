# Issue

**Title:** feat: add density map support to Xenium Explorer transcript writer

## Description

## Summary

While making paper figures I noticed that the density map toggle in Xenium Explorer v4.0+ no longer works with SOPA-converted data, though it worked in Explorer <4.0. Investigation revealed that `write_transcripts()` in `sopa/io/explorer/points.py` only writes the `grids/` group, but native Xenium `transcripts.zarr.zip` files include additional arrays that Explorer v4+ requires for the density map.

### What's missing vs native Xenium format

| Group | Purpose |
|---|---|
| `density/gene/` | Pre-computed transcript density as CSR sparse matrix (10µm bins) |
| `density/codeword/` | Per-codeword density (same CSR format) |
| `gene_category` | Boolean matrix (n_genes × 9) classifying genes as gene/neg_control/blank/etc |
| `codeword_category` | Boolean matrix (n_codewords × 9) for codewords |
| `metrics_density` | Float32 3D array (y_bins × x_bins × 4) of QC density metrics (20µm bins) |

### Changes

- **`sopa/io/explorer/points.py`**: Added `_write_density()` and `_classify_gene_names()` helper functions. `_write_density()` is called at the end of `write_transcripts()` to write all missing arrays into the zarr group.
- **`sopa/io/explorer/_constants.py`**: Added `DENSITY_GRID_SIZE` (10µm) and `METRICS_DENSITY_SPACING` (20µm) constants.

No version bump, no new dependencies (uses `scipy.sparse` which is already a SOPA dependency), no changes to `converter.py` or any other file.

### How it was verified

- Downloaded native Xenium tiny datasets from 10x Genomics (XOA 3.0 Mouse Ileum, XOA 4.0 Human Ovary) to map the exact zarr structure
- Generated a SOPA explorer output from an in-house CosMx dataset, then patched in the density arrays
- Confirmed the density map toggle works correctly in Xenium Explorer with the patched output

Claude was used to help with the coding part.

## Test plan

- [x] Open a SOPA-generated `.explorer` output in Xenium Explorer v4.0+ and verify the density map toggle works
- [x] Verify transcript points still display correctly (no regression)
- [x] Test with Xenium, CosMx, and MERSCOPE data if available

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b592051d64ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.