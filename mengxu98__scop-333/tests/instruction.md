# Issue

**Title:** fix: harden live spatial backend adapters

## Description

## Summary

This PR hardens the four spatial adapters that failed or produced incomplete evidence against their current live backends. It does not add dependencies, public APIs, backend substitutes, environment switches, or global options.

- **CARD/CARDspa**: preflights backend-selected informative genes, runs only supported spots, restores the full input spot identity, and records unsupported informative-zero spots as explicit `NA` rows in the stored proportions and metadata.
- **SpatialCellChat**: isolates upstream progress/future helpers so backend execution does not mutate global handler state, repairs sparse 3D conversion for the current backend, and retains valid pathway-level probabilities when ligand-receptor table extraction is unavailable. The stored result declares whether it is ligand-receptor or pathway level.
- **SpatialEcoTyper**: supplies missing dplyr/tidyselect/magrittr symbols only in locally reconstructed backend closures, without modifying package namespaces or the returned SCOP object.
- **SpatialQM**: checks the actual GitHub repository, filters arguments against installed metric formals, maps finite metadata coordinates into the temporary backend object, changes the default to three live object-first metrics, and reports the actual backend cause when all selected metrics fail.

All optional repositories still use `check_r()` and `get_namespace_fun()` at runtime. No optional backend was moved into Imports/Depends/Suggests.

## Live-backend evidence

The adapters were run through public SCOP entry points on real spatial objects before publication:

| Wrapper | Backend | Live result |
|---|---|---|
| `RunCARD()` | CARDspa 1.2.1 | raw and `legacy_display` both succeeded; 428/428 spot identity preserved, 422 supported spots plus 6 explicit `NA` spots |
| `RunSpatialCellChat()` | SpatialCellChat 0.1.0 | 7/7 cell/spot/composition, auto, C++/R mode combinations succeeded; 74-cell and 422-spot identities preserved |
| `RunSpatialEcoTyper()` | SpatialEcoTyper 1.0.4 | single, recovery and deconvolution modes succeeded; strict multi-sample mode failed atomically for missing assignments, while `allow_partial` retained 444 assignments and 6 explicit missing values |
| `RunSpatialQM()` | SpatialQM 0.1.0.9000 | default `n_cells`, `tx_per_cell`, `max_detection` run succeeded on 500 Xenium cells; 4/14 individually requested metrics succeeded and 10 current upstream/data limitations were returned explicitly without fallback substitution |

Every successful run checked input identity, output identity, schema-v1 storage and provenance. Every expected failure checked that the input object remained unchanged.

## Validation

- `pkgload::load_all(".", quiet = TRUE, compile = FALSE)`
- 34 existing spatial test files, 222 expectations: **pass**
- modified R and test files: **parse**
- generated `RunSpatialQM.Rd`: `tools::Rd2ex()` + `parse()`: **pass**
- tarball-based `rcmdcheck --no-manual --as-cran --no-examples --no-tests`: **0 errors / 0 warnings / 4 existing notes**
- `checking dependencies in R code ... OK`
- `checking for unstated dependencies in examples ... OK`
- `git diff --check`: **pass**

The remaining check notes are pre-existing repository metadata/time/heatmap static-analysis notes and are outside this spatial adapter PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3d888f5c3fe0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.