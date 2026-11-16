# Issue

**Title:** Update clone color handling in plotCNVTree function and documentation

## Description

## Summary
This PR refactors the CNV clustering logic to prevent execution errors on small datasets and enhances color palette handling across visualization functions to support consistent multi-dataset analysis.

## Changes
### 1. Clustering logic improvements

- **Conditional Evaluation:** Optimized the workflow to perform k value evaluation only when `kDetection == "automatic"`. This prevents unnecessary computation and potential crashes when a manual k is specified.

- **Dynamic `k` Range:** Fixed a "hardcoded range" bug where evaluation attempted to test `k_values <- 1:15` regardless of the number of available nodes.

``` R
[2026-04-15 11:10:59] Aggregating counts matrix...
[2026-04-15 11:11:10] Done !
[2026-04-15 11:11:10] Running CNV analysis...
Using genes data from ensembl version 113.
[2026-04-15 11:11:22] Done !
[2026-04-15 11:11:22] Computing CNV per chromosome arm...
[2026-04-15 11:11:23] Done !
[2026-04-15 11:11:23] Clustering CNVs...
Error in cutree(hc, k = k) : elements of 'k' must be between 1 and 14
```
The maximum  `k` is now dynamically set to `min(15, length(hc$order) - 1)` to avoid such errors.

### 2. Visualization & Color Palette Handling
 - **Named Palette Support** (`plotCNVResults` / `plotCNVResultsHD`):
    - **Previous:** `referencePalette` names were ignored, and colors were reassigned based on the order of appearance in the annotation data.frame. 
    - **New Behavior:** Functions now respect named color palettes. This allows users to enforce a unified color scheme across different patients or datasets.

- **Robust Clone Coloring** (plotCNVTree):
   - **Previous:**  the function discarded the entire palette if the length didn't match the clone count exactly.
   - **New Behavior:** The function now validates that the palette has at least enough colors and subsets it as needed. This allows the use of a large, master palette across multiple objects.

- Documentation: Updated .Rd files for `CNVtree` and `plotCNVtree` to clarify the requirements for custom clone_cols.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6806f6b2dc12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.