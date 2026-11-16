# Issue

**Title:** Use scTenifoldKnk 2.0 for knockout analysis

## Description

Replace the duplicated knockout implementation with the official scTenifoldKnk 2.0 workflow. QC, CPM normalization, network construction and statistics now follow upstream while scop retains Seurat inputs, result storage and existing plots.

- Add heat alignment, response directions, transcriptome-wide screens and seed controls.
- Remove the local C++ kernels, native exports, redundant helpers and obsolete acceleration notes; update documentation and tests.
- Declare scTenifoldKnk >= 2.0.0 and scTenifoldNet as optional CRAN dependencies without new GitHub Remotes. Add six required CRAN lockfile records while preserving all 174 existing records.

Compatibility: remove `backend` and replace `qc_min_cells` with the upstream fraction parameter `qc_min_pct`. Existing saved differential-regulation tables remain plottable. Heat alignment has no manifold coordinates, and transcriptome-wide results are stored as perturbation matrices.

Validation on macOS with R 4.5.3, scTenifoldKnk 2.0.0 and scTenifoldNet 1.4.3:
- Package build and installation succeeded; removed native registrations are absent.
- 67 module assertions and 27 shared sparse-path assertions passed.
- Complete manifold and heat outputs on the bundled pancreas data (301 genes, 1,000 cells) were identical to direct upstream calls.
- Dependency scanning and before/after lockfile checks completed; all 44 packages in the required runtime closure match in version and source. Full-project renv status retains pre-existing unrecorded packages outside this scope.

Other platforms have not been validated locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ebc3b0c3ef8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.