# Issue

**Title:** build(io): replace pyreadr with rdata

## Description

Is related to  but fully switches from pyreadr to rdata

`pyreadr` is AGPL-3.0, which blocks commercial use of infercnvpy. `read_scevan` now reads SCEVAN `.RData` files with `rdata` (MIT, pure Python).

- `pyproject.toml`: swap the `pyreadr` dependency for `rdata`.
- `io/_scevan.py`: add `_read_rdata_frame`, which returns a DataFrame whether `rdata` produces a data frame or a matrix with row and column names. `read_scevan` behaves as before.

### Validation

Checked manually, since CI has no SCEVAN output to run against:

- Ran `SCEVAN::pipelineCNA` 1.0.3 on the bundled oligodendroglioma dataset (184 cells, 4 subclones) and loaded the real `*_CNAmtx.RData`, `*_CNAmtxSubclones.RData` and `*_count_mtx_annot.RData` with `read_scevan`. `obsm["X_scevan"]` equals SCEVAN's `CNA_mtx_relat` exactly, and the tumor/normal and subclone labels and chromosome positions are correct.
- `rdata` read 15 of 16 R-written matrices from the SCEVAN paper's synthetic benchmark. Values match R's own export to about 5e-15 (the 16th file is truncated and fails in R too). `pyreadr` raised `IndexError` on all 16.

— Claude Code (AI assistant), posted on behalf of @stephenwilliams22

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc22bc4e6861`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.