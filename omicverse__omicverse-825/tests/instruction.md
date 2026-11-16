# Issue

**Title:** feat(single): integrate py-Augur cell type prioritization as ov.single.Augur

## Description

## Summary

Integrate [py-Augur](https://github.com/omicverse/py-Augur) into `omicverse.single`, exposing `ov.single.Augur` — a machine-learning-based cell type prioritization tool that ranks cell types by their transcriptomic response to experimental perturbations.

Augur trains a random-forest or logistic-regression classifier per cell type to predict condition labels, evaluates AUC via stratified cross-validation, and ranks cell types accordingly (higher AUC = stronger perturbation response). Based on Skinnider et al. 2020, *Nature Communications*.

## What's added

### `omicverse/single/_augur.py` (new, ~1220 lines)
- `Augur` class following the CNV/Metabolism pattern (stateful class + `run()` + `@register_function`)
- Core ML pipeline: stratified subsampling, variance-based feature selection, RF/LR classifiers, AUC/CCC metrics
- Differential prioritization via permutation testing
- 6 visualization functions adapted to omicverse style (sc_color palette, clean spines, no default titles):
  - `plot_lollipop()` — AUC ranking
  - `plot_umap()` — UMAP overlay colored by AUC
  - `plot_important_features()` — top gene importance
  - `plot_augur()` — combined lollipop + features
  - `plot_scatterplot()` — compare two runs (shows all cell type labels by default)
  - `plot_differential_prioritization()` — differential results

### `tests/test_augur.py` (new, 11 tests)
- Basic run, result structure, `adata.uns` / `adata.obs` storage
- Logistic regression classifier, velocity mode
- Plot function return values, method chaining
- Error handling (plot before run)

### `omicverse/single/__init__.py` (modified, +2 lines)
- `from ._augur import Augur` + `'Augur'` in `__all__`

## Demo results

Synthetic dataset: 800 cells, 6 cell types, signal strength 0.35–0.8 std (10–30 genes).

| Cell type | AUC |
|-----------|-----|
| CD8+ T | 0.845 |
| Monocyte | 0.675 |
| DC | 0.638 |
| CD4+ T | 0.562 |
| B cell | 0.518 |
| NK cell | 0.513 |

### Visualizations

**Lollipop Plot** — AUC ranking
![augur_lollipop](https://raw.githubusercontent.com/Zac-lzh/omicverse/feat/augur-integration/sample/augur/augur_lollipop.png)

**UMAP Overlay** — colored by AUC
![augur_umap](https://raw.githubusercontent.com/Zac-lzh/omicverse/feat/augur-integration/sample/augur/augur_umap.png)

**Important Features** — top genes
![augur_features](https://raw.githubusercontent.com/Zac-lzh/omicverse/feat/augur-integration/sample/augur/augur_features.png)

**Combined Plot** — AUC + features
![augur_combined](https://raw.githubusercontent.com/Zac-lzh/omicverse/feat/augur-integration/sample/augur/augur_combined.png)

**Scatter Plot** — compare two runs (all cell types labeled by default)
![augur_scatter](https://raw.githubusercontent.com/Zac-lzh/omicverse/feat/augur-integration/sample/augur/augur_scatter.png)

## Output schema

```
adata.uns['augur'] = {
    'AUC': DataFrame[cell_type, auc],       # or 'CCC' for regression
    'results': DataFrame[per-subsample/fold metrics],
    'feature_importance': DataFrame[gene-level importance],
    'parameters': dict[run configuration],
}
adata.obs['augur_auc'] = per-cell AUC mapped from cell_type
```

## Result parity

Verified: `ov.single.Augur.run()` produces **identical AUC values** to standalone `pyaugur.calculate_auc()` on the same input (same seed, same parameters).

## Usage

```python
import omicverse as ov

augur = ov.single.Augur(adata, label_col='condition', cell_type_col='cell_type')
augur.run(n_subsamples=50, subsample_size=20, folds=3)
augur.plot_lollipop(title="Cell Type Prioritization")

# Compare two conditions
dp = augur.run_differential(adata2, n_permutations=1000)
augur.plot_differential_prioritization(dp)
```

## Test plan

- [x] `python -c "import omicverse as ov; print(ov.single.Augur)"` resolves
- [x] `pytest tests/test_augur.py` — 11/11 pass (Python 3.10+)
- [x] AUC parity with py-Augur on synthetic data (seed=42, n_subsamples=5, folds=2)
- [x] flake8 E9/F63/F7 — no syntax errors

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b4428afae8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.