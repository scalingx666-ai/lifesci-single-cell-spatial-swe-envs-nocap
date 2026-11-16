# Issue

**Title:** Extend RunDorothea network inputs and CollecTRI support

## Description

## Summary

- extend `RunDorothea()` to accept `NULL`, `"dorothea"`, `"collectri"`, and custom regulatory network tables
- connect standardized `RunGRN()` output (`TF`, `target`, `importance`) directly to TF activity inference
- normalize supported regulator and weight aliases while preserving signed versus unsigned semantics and provenance
- resolve optional `decoupleR` functions through `check_r()` and `get_namespace_fun()`
- make `DorotheaPlot()` network-aware and avoid signed activation/repression labels for unsigned networks
- add synchronized documentation and regression coverage

## Why

`RunGRN()` returns `TF`, `target`, and `importance`, while `RunDorothea()` previously required `tf`, `target`, and `mor`. This prevented SCOP GRN results from flowing directly into the existing activity assay and plotting workflow. CollecTRI was also unavailable through the public entry point.

## User impact

Existing DoRothEA calls and the `dorothea` assay/tool names remain compatible. Users can now pass a `RunGRN()` result directly or select CollecTRI with `regulons = "collectri"`. Unsigned importance networks are explicitly recorded as target-program activity and are not presented as activation/repression evidence.

## Validation

- `pkgload::load_all(".", quiet = TRUE, compile = FALSE)` passed
- generated `RunDorothea.Rd` and `DorotheaPlot.Rd` examples passed `Rd2ex()` plus `parse()`
- focused Dorothea suite: 38 assertions passed; one pre-existing heatmap test remains blocked in this Windows environment because `heatmap_border_color` is unavailable from the installed plotting runtime
- real custom `TF`/`target`/`importance` input completed through the installed `decoupleR::run_ulm` backend and produced a 2 x 3 score matrix
- package check without installation completed with 0 errors, 0 warnings, and 1 inherited CRAN note; no dependency-in-code or unstated-example dependency warning was introduced

## External integration note

The live CollecTRI retrieval attempt reached the installed `decoupleR`/`OmnipathR` path but failed inside the current `OmnipathR` fallback (`unnest_evidences`: `.keep` has length zero). CollecTRI adapter behavior and human/mouse mapping are covered by mocked unit tests; this draft does not claim a successful live OmniPath retrieval in the current environment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `addc66f309cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.