# Issue

**Title:** Add COZI to nhood_enrichment()

## Description

## Description

- Adds `normalization` parameter for conditional and total normalization of neighbor counts to `nhood_enrichment()` as described in [*Schiller et al bioRxiv*](https://doi.org/10.1101/2025.03.31.646289).  
- Adds conditional cell ratio (CCR) output when `normalization`= `conditional`. CCR is the proportion of cells of an index type that neighbors cells of the neighbor type. 
- Adds `nhood_enrichment_dotplot()`to plot zscore and CCR at once.
- Adds `min_cell_count` parameter to `nhood_enrichment()` to filter out clusters of cells with counts below the set threshold. Filtered out interaction z-scores are replaced with NA. 

## How has this been tested?

Added additional test functions for nhood_enrichment with conditional normalization and CCR. Test images for dotplot are missing, all other tests run successfully.

## TODO

- [x] Add dotplot test images for test

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a04f5884aa7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.