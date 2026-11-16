# Issue

**Title:** Add Differential Expression Analysis Module

## Description

## Description
This PR introduces a new differential expression analysis module for SingleRust, providing functionality similar to Scanpy's `sc.tl.rank_genes_groups()`. The implementation allows users to identify genes that are differentially expressed between groups of cells.

## Features
- `rank_gene_groups` function that works with AnnData objects in memory
- Support for multiple test methods (t-test, Mann-Whitney)
- Multiple correction methods for p-values (Bonferroni, Benjamini-Hochberg, etc.)
- Calculation of log fold changes
- Customizable reference group selection
- Results stored in the `uns` attribute of the AnnData object

## Implementation Notes
- This is an experimental implementation not fully compatible with the Scanpy version yet
- Storage format differs from Scanpy as rec-arrays are not implemented in the Rust version of AnnData
- Results are stored as DataFrames in the `uns` attribute instead of structured arrays

## Testing
- Added basic unit tests with synthetic data to validate functionality
- Tests verify correct storage and basic statistical properties

## Future Work
- Improve compatibility with Scanpy's implementation
- Add support for additional test methods (negative binomial, etc.)
- Optimize performance for large datasets
- Enhance documentation and examples

## Breaking Changes
None. This is a new feature that doesn't modify existing functionality.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b17a5eacf8f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.