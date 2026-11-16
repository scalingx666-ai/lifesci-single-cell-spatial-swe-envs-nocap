# Issue

**Title:** Data checks

## Description

- **Version bump**: The package version is updated from 0.6.1 to 0.6.2.
- **Enhanced data validation**: New functions are added to cytetype/anndata_helpers.py to:
  - Detect if gene symbol columns actually contain gene IDs (e.g., Ensembl, RefSeq, numeric, or other database-style IDs).
  - Warn the user if a high proportion of entries appear to be IDs instead of human-readable gene symbols.
  - Integrate this validation into the AnnData validation pipeline.
- **Stronger error handling in marker extraction**: The marker gene extraction logic now raises explicit errors if no marker genes are found for any group and logs warnings for empty groups.
- **Client polling improvements**: The initial polling delay in result polling is increased from 10 to 20 seconds, with improved user-facing log messages.
- **Code cleanup**: Redundant or duplicate logging is removed from the main module.
- **Expanded test coverage**:
  - Extensive new and updated tests for the new gene symbol validation routines, error conditions, and edge cases.
  - New test modules for missing functionalities in anndata_helpers and client logic.
  - Additional tests for config constants and custom exceptions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bf2e9cfc506d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.