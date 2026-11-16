# Issue

**Title:** Fix pandas 3.0 tokenizer crash; document perturb extra; improve tutorials

## Description

## Summary

Fixes the pandas 3.0 crash in tokenization, documents the `perturb` extra, and improves the perturbation / spatial-mapping tutorials based on user testing feedback.

### Code fix (the important one)
- `src/terra/tokenizers/cell_tokenizers.py` (lines 817, 1537): use `.iloc[coding_miRNA_idx]` for positional gene selection instead of `adata.var['ensembl_id'][coding_miRNA_idx]`. pandas 3.0 removed the positional-integer fallback for `Series.__getitem__` (it is now label-based), so the old code raised `KeyError: None of [Index([...])] are in the [index]` during `tokenize_adata` on any fresh install (which pulls pandas 3.0). `.iloc` works on pandas 2.x **and** 3.0. Verified end-to-end tokenising the full 123k-cell section on pandas 3.0.3 / Python 3.12.

### Docs
- `docs/installation.md`: add the `perturb` extra (GeomLoss) to the optional-extras table — it is required by the perturbation and spatial-mapping tutorials, and installing plain `terra-st` otherwise fails with an `ImportError` from `infer_token_distance`.
- `docs/notebooks/perturbation_tutorial.ipynb` and `spatial_mapping_tutorial.ipynb`:
  - walk-through explanations per step (what / input / output / how to read the result);
  - per-step timing warnings (tokenise CPU-bound; per-cell distance GPU; A100 numbers + H100 placeholders to fill);
  - reduced saved-figure DPI 1200 -> 300;
  - removed the redundant `!pip install` cell and pointed the Requirements note to the installation guide (kept `gdown`); added a Colab / fresh-env `%pip install "terra-st[perturb]" gdown` cell and a note that geomloss is required.

### Notes
- No dependency caps added — the `.iloc` fix makes the code pandas-2/3 compatible, so pandas is not pinned.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c2e3b827e99`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.