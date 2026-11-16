# Issue

**Title:** fix(ci): resolve optional dependencies and install test runtimes

## Description

## Why

The optional-dependency CI job fails before tests because automatic pandoc detection resolves every Suggests entry, including two GitHub-only packages. The platform test jobs also omit packages used by the plotting, scoring and differential-accessibility tests.

## What changed

- Keep monocle3 and SeuratData outside DESCRIPTION dependency fields. Preserve the existing runtime GitHub checks and data provenance.
- Declare Hmisc and lmtest as optional dependencies, check Hmisc when constructing bar summaries, and record only the missing Hmisc dependency closure.
- Use the yaGST repository with repaired DESCRIPTION metadata for SCEVAN installation. Install directly from Yunuuuu/yaGST without a commit suffix.
- Reject unsupported fastCNV genomes before dependency installation, with a regression assertion that dependency checks are not reached.
- Provide the official satijalab/seurat-wrappers repository for fastCNV when the resolver does not carry its transitive Remotes source. Use the repository directly without a commit suffix.
- Install the six required test-runtime packages in check and coverage jobs. Set up pandoc before the optional-contract dependency step.

- Qualify `utils::tail()` in the CNV chromosome strip helper and remove redundant `loadNamespace("DOSE")` calls from enrichment tests that already use `skip_if_not_installed()`. This clears the package-check NOTE and the undeclared test dependency WARNING.
- Align the `...` documentation of `RunCNV()` and `CNVPlot()` with the rest of the package.

## Scope

Preserve algorithms, plotting summaries, assertions and optional-backend validation. No new test skips or unrelated dependency upgrades.

## Verification

- Reproduced the dependency solver failure, then resolved all 150 direct dependencies after the change.
- Ten relevant test files pass 806 assertions with zero failures, errors or skips. Existing upstream diagnostic warnings remain visible.
- The new summary-dependency regression fails before the fix and passes afterward. Existing lock records and repository metadata are unchanged.
- The full documentation dependency manifest resolves all 169 package specifications without consulting an installed package library. The verified yaGST source matches nine function definitions and three complete numerical outputs; 154 CNV assertions pass.
- The previous head (6b4fa682) passed every GitHub Actions check, including the full 382-topic/17-article pkgdown build. Platform assertions passed: macOS 10,475; Linux 11,084; Windows 10,333.
- After removing runtime commit suffixes, all 169 website dependency specifications resolve with lib=NULL, all 154 CNV assertions pass, and the actual documentation scanner emits the direct repository specifications. The installed-source renv records remain unchanged.
- The CNV strip labels are identical before and after qualification for 5, 13, 14, 23 and 24 chromosomes. CNV, enrichment word cloud and GSEA layout tests pass 201 assertions with zero failures, errors, warnings or skips. The R CMD check test-dependency scan reports no undeclared packages.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1fbd12dd856a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.