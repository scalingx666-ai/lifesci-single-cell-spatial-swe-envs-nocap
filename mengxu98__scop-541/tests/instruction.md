# Issue

**Title:** Fix Harmony RNA layer preservation and marker feature mapping

## Description

Harmony preprocessing could restrict RNA expression layers to shared genes when libraries had different feature sets. Preserve complete RNA layers and ordered per-library cached variable features, and read marker matrices through LayerData so partial feature and cell maps remain valid.

Extend the existing regression coverage for four-library counts preservation, cached HVF reuse, the complete StandardWorkflow-to-Harmony pipeline, and marker parity with Seurat. Install Harmony in the main CI matrix so the integration regression runs.

Locally, 34 tests passed across five related test files; one optional Python interoperability test was skipped because anndata and scipy were unavailable. The merged-input cached HVF control matched the previous behavior, and the CI YAML and diff checks passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8811fce70329`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.