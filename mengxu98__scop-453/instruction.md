# Issue

**Title:** fix: use speckle for propeller proportion tests

## Description

`proportion_method = "propeller"` previously used an internal logit-transformed t-test, so its P-values and FDR did not match speckle propeller. This change delegates proportion transformation and empirical Bayes moderated testing to speckle's `getTransformedProps()` and `propeller.ttest()`, with upstream defaults for `transform`, `robust`, and `trend`.

Fully paired comparisons use a donor-blocked design; partial pairing and insufficient replication are rejected. SCOP retains pairwise comparisons, descriptive proportion-ratio effects, and sample bootstrap intervals. Results record backend provenance and design matrices, virtual samples mask both standardized and raw inferential statistics, and plots distinguish new speckle results from previously stored internal-test results. The optional backend uses `check_r()` and `get_namespace_fun()` without adding DESCRIPTION dependencies or behavior switches. Roxygen and Rd documentation are synchronized.

Validation:
- 116 assertions passed with no test failures or warnings, including all eight transform/robust/trend combinations, zero/one proportions, unequal sample totals, paired upstream comparisons, comparison reversal, bootstrap reproducibility, virtual-sample masking, and existing abundance contracts. Repeated after rebasing onto current main (`c364fa0e`).
- Tested against speckle 1.10.0 and limma 3.66.0; the representative synthetic input has zero absolute difference from upstream in P-values, FDR, and t statistics.
- `pkgload::load_all(".", quiet = TRUE, compile = FALSE)` passed. The source package compiled and installed successfully, and installed-package regression tests also passed.
- The prescribed no-examples/no-tests `--as-cran` check completed. After updating thisplot/thisutils in an isolated validation library, a follow-up check reused the successful installation with `--no-install --library=...`: 0 errors, 1 warning, 4 notes. R-code dependency checks passed; the full check's unstated-example-dependency check also passed. The remaining warning concerns undocumented arguments in the unchanged `RunSingleR.Rd`.

Compatibility: Existing propeller analyses must be rerun because the statistical method has changed. Multiple conditions continue to produce pairwise tests; this does not introduce speckle's omnibus ANOVA interface. Bootstrap intervals describe the proportion ratio and are not moderated-test intervals.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `790c367fc400`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.