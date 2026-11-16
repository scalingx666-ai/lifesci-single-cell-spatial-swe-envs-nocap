# Issue

**Title:** Add `normalized` flag to Preprocessor to skip normalization

## Description

Reimplements the intent of #601 (closed: stale base) on current master.

## Summary
Adds a `normalized: bool = False` argument to `Preprocessor`. When set to `True`, the three normalization steps — `_normalize_by_cells`, `_normalize_selected_genes`, and the `norm_method` transform — are skipped (each logs an info message), while filtering, gene selection, regression and PCA still run. This lets users feed already-normalized data through the Preprocessor without double-normalizing.

## Usage
```python
preprocessor = dyn.pp.Preprocessor(normalized=True)
preprocessor.preprocess_adata(adata, recipe="monocle")
```

## Validation
Verified on a synthetic AnnData: with `normalized=True`, `adata.X` is left unchanged (raw counts preserved) and all three skip-messages fire.

Closes the goal of #601.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01AD7gAdxa3Zt5uiQVDoANa5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eddcc31c8f76`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.