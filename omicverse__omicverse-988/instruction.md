# Issue

**Title:** feat(single): add optional Scissor cell-selection adapter

## Description

## Summary

Add `ov.single.Scissor` for phenotype-associated cell selection through the independent `scissor_py` backend. Importing OmicVerse and constructing the adapter work without the backend; `run()` checks it lazily and gives a reproducible installation command pinned to the published organization commit .

The existing candidate was adapted to current `master` (`e4dcff8`). Changes are one thin adapter, two import/export lines, and ten focused tests. Numerical solvers, preprocessing and graph creation remain in the independent backend or the caller's workflow. The full notebook is contributed separately to `omicverse/omicverse-tutorials`; no tutorial is added to this repository.

```python
model = ov.single.Scissor(
    adata, bulk=bulk, phenotype=phenotype, family="binomial",
    layer="lognorm", graph_key="connectivities", positive_label="mutant",
    semantics="corrected",
)
result = model.run(alpha=None, cutoff=0.2, random_state=123, foldid=foldid)
```

The adapter requires explicit bulk phenotypes, expression-layer selection and an existing cell graph. Successful runs write aligned labels, coefficients and an H5AD-safe audit record. Collisions fail unless `overwrite=True`; failed runs preserve prior annotations and `result_`. `official` remains the default numerical semantics; `corrected` is an explicit scientific choice. The backend is GPL-3.0-or-later, requires Python >=3.10, and normally runs without R. No dependency auto-install or data download is added.

## Validation

- Actual source-tree OmicVerse import and class construction with **no scissor_py installed** succeeded; `run()` produced the intended missing-backend error.
- `python -m pytest tests/single/test_scissor.py -q`: **10 passed**, including three families × X/named layers, ID/class alignment, H5AD roundtrip, collision handling and dependency errors.
- Existing candidate integration suite against installed OmicVerse 2.3.2 and the backend installed from the pinned organization commit: **18 passed**, including registry resolution and failed-input rollback. No OmicVerse module stubs were used.
- All seven tutorial code cells completed in an actual local Jupyter kernel. Gaussian, Binomial and Cox wrapper coefficients exactly matched direct backend calls; all six result namespaces survived H5AD save/reload.
- Published backend: **403 local Windows tests passed**, wheel/sdist boundaries passed, and [Linux/Windows CI passed](https://github.com/omicverse/py-Scissors/actions/runs/38209843307).

Validation used private caches and a process-local external-network guard. Existing OmicVerse analytics/import behavior is unchanged. Focused tests emitted existing pytest-option, AnnData deprecation and sparse-efficiency warnings; the complete OmicVerse suite was not run. Synthetic interface verification does not establish biological or clinical efficacy or complete equivalence to the original Seurat workflow.

## Companion contributions

- Adapter: 
- Tutorial: 
- Skill:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1155a38476da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.