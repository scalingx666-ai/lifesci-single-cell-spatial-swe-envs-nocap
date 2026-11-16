# Issue

**Title:** feat(pl): display-only clipping (umi_clip_at / gene_clip_at) in ov.pl.qc

## Description

## Summary

Implements the  request: a **display-only** max-range clip for the UMIs- and genes-per-cell panels of `ov.pl.qc`, so a handful of extreme-high-count cells no longer compress the distribution of the rest.

```python
ov.pl.qc(adata, umi_clip_at=50000, gene_clip_at=8000)
```

- `umi_clip_at` clips the UMI/count metrics (`nUMIs`, `total_counts`); `gene_clip_at` clips the gene-count metrics (`detected_genes`, `n_genes_by_counts`).
- **Display only** — `adata.obs` is never modified; the underlying data / filtering logic is unchanged.
- Works for histogram and violin panels, and for grouped plots (`batch_key`).
- Validates clip values (positive numeric or `None`) and labels a panel as clipped.

## Credit

Implementation **contributed by @Flynn2059**, who wrote and validated the patch in https://github.com/Flynn2059/omicverse-qc-clip-patch — applied here verbatim. Thank you! 🙏

## Tests

`tests/pl/test_qc.py` — **16 passed** (incl. confirmation that `adata.obs` is not modified). flake8 (E9,F63,F7) clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0ffe0d4aabe5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.