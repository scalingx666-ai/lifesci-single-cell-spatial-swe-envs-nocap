# Issue

**Title:** SPLIT v0.2.0: Annotation-method agnostic purification

## Description

This PR introduces a major update to SPLIT, making it fully independent of RCTD as the annotation backend while maintaining complete backward compatibility with existing RCTD-based workflows.

---

**What's changed**

- **New core function** `rctd_free_purify()`: a standalone purification function that accepts any deconvolution result. Requires a cells × cell-types weight matrix, a genes × cell-types reference matrix, and optionally a primary cell-type vector (inferred as argmax of weights if not provided).
- **Updated `purify()` wrapper**: automatically dispatches to `rctd_free_purify()` or the legacy RCTD-based path depending on the input. The `rctd` argument remains fully supported.
- **New helper** `convert_rctd_result_to_purify_input()`: extracts deconvolution weights, primary cell-type vector and reference matrix from RCTD output for use with the new agnostic interface.
- **Full-transcriptome compatible**: validated on ATERA (~18,000 genes); runs to completion in minutes.
- **Reduced dependencies**: `spacexr` and `BiocParallel` moved from `Imports` to `Suggests`; `S4Vectors` and `SingleCellExperiment` added to `Imports`.
- **New vignette**: comparison of ATERA and Xenium with SPLIT purification applied to both.
- **Updated `NEWS.md`, `README.md`, `CITATION`, and `DESCRIPTION`** to reflect the new release and updated journal reference (Nature Methods, 2026).

---

**Backward compatibility**

All existing code using `purify(counts, rctd = RCTD)` continues to work without any changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5afbd6995694`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.