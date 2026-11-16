# Issue

**Title:** fix(spatial): make C-SIDE storage messages truthful

## Description

## Summary
Only announce detailed result storage when it occurred. Preserve compatibility metadata and existing saved results with store_results=FALSE. Document n_sig as a run-level significant record count, not a unique-gene count or local effect.

## Validation
- Focused tests passed; all nine combined regression files also passed after merging current upstream main 73cee6135 into an isolated verification worktree.
- Native gradient/observed-neighborhood entry points were exercised. C-SIDE coverage uses adapter mocks; live spacexr was not revalidated.
- Final Windows package check completed: **0 errors, 2 warnings, 4 notes**, using --no-manual --as-cran --no-examples --no-tests and _R_CHECK_FORCE_SUGGESTS_=false.
- Warnings are in unchanged baseline code/docs: undeclared lifecycle calls in R/PseudobulkExpression.R; undocumented arguments in CellDimPlot3D.Rd, FeatureDimPlot.Rd, IntegrationBenchmarkPlot.Rd, and RunIntegrationBenchmark.Rd. This is not a warning-free check.
- Unstated dependencies in examples: OK. Code/documentation mismatches: OK. Changed Rd extraction/parsing and git diff --check: passed.
- Initial Windows temporary-library reparse-point errors were resolved with task-local D: temporary storage. No dependency bypasses, optional backend switches, or global package options were added.
- pkgdown passed on GitHub; three-platform R CMD check is still pending at the time of this update.

## Integration
Independent branch based on d6646dc; current upstream changes were checked in the combined validation worktree. Source changes do not depend on the other two PRs. Merging the three may require trivial reconciliation of their NEWS entries. Existing user worktree edits and the installed D: library were not modified.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `259132b12527`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.