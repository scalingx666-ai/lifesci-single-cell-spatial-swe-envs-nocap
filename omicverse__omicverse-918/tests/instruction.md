# Issue

**Title:** fix(space): replace legacy rpy2 mclust wrappers

## Description

## Summary

- add a shared, lazy `pymclustR` adapter with input/result validation and NumPy RNG-state restoration
- replace legacy embedded `rpy2`/R `mclust` calls in PROST, GraphST, STAGATE, STAligner, and BINARY while preserving their public contracts and 1-based labels
- fix `ov.utils.cluster(method="pymclustR")` so `key_added` and legacy `add_key` select the output column instead of leaking into `Mclust()`; conflicting values fail clearly
- add `pymclustR>=0.2.1` to the `full` and `tests` extras while keeping it lazy and optional for base installations

## Root cause and compatibility

PR #638 introduced the Python mclust backend for the generic clustering utility, but five spatial wrappers still embedded separate `rpy2`/R implementations. Reusing the generic entry point directly would also have changed established spatial output-key behavior and exposed the `add_key` parameter leak.

This PR centralizes only the backend mechanics. Existing spatial APIs remain unchanged:

- PROST still returns the label array
- GraphST, STAGATE, and STAligner still write categorical `adata.obs["mclust"]`
- BINARY still respects arbitrary `add_key`
- `ov.utils.cluster()` still modifies AnnData in place, returns `None`, defaults to `adata.obs["pymclustR"]`, and stores fit metadata under `adata.uns["pymclustR"]`
- labels retain R mclust's 1-based semantics

`tradeSeq` is intentionally out of scope; it should be handled separately only after real R-to-Python numerical parity validation.

## Validation

- focused spatial/pymclustR suite: 22 passed
- focused suite plus import/architecture tests: 429 passed
- exact parity against direct `mclust_py.Mclust` for classification, model name, G, log-likelihood, and BIC
- all five wrappers exercised with the real Python backend
- global NumPy RNG restoration, missing dependency, invalid input, key alias/conflict, and no-parameter-leak coverage
- fatal flake8 syntax gate (`E9,F63,F7`): passed
- wheel build and installed-wheel smoke test: passed
- wheel metadata contains the optional dependency in both extras
- diff whitespace check: passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `23a4ebe3e19f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.