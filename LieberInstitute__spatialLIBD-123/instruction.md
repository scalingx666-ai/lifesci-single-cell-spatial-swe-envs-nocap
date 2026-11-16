# Issue

**Title:** edit scuttle to scrapper for aggregateAcrossCells()

## Description

We noticed that the package test was breaking [[here](https://github.com/LieberInstitute/spatialLIBD/actions/runs/30098713591/job/89499122353#step:19:156)] after the warning message:

`Warning in .local(x, ...) : 'aggregateAcrossCells' is deprecated.`

The `aggregateAcrossCells()` function in the `scuttle` package is being phased out in favor of the new `scrapper` package (]()) and has also been replaced in recent Bioconductor updates, such as in `imcRtools` ([[Bioconductor 3.23 Release](https://www.bioconductor.org/news/bioc_3_23_release/)]. Additionally, internal arguments such as `average` have been deprecated in favor of `statistics` [link](https://rdrr.io/bioc/scuttle/man/aggregateAcrossCells.html).

### Implementation

The initial implementation directly replaced `scuttle::aggregateAcrossCells()` with `scrapper::aggregateAcrossCells()`. However, the two functions work differently.

`scuttle::aggregateAcrossCells()` accepts a `SingleCellExperiment` and returns a `SingleCellExperiment`, while the `scrapper::aggregateAcrossCells()` implementation currently available to us operates on a matrix-like input and returns a list containing the aggregated counts and grouping information (`sums`, `detected`, `combinations`, `counts`, and `index`).

Therefore, directly passing the `SingleCellExperiment` to `scrapper::aggregateAcrossCells()` resulted in:

`Error in dim(x) <- length(x) : invalid first argument, must be vector (list or atomic)`

The implementation was updated to aggregate the `counts` matrix with `scrapper::aggregateAcrossCells()` and reconstruct the `SingleCellExperiment`. The original `colData` is also reconstructed, preserving the original column types and retaining the grouping variables (`registration_variable`, `registration_sample_id`) and `ncells`, to reproduce the structure of the previous `scuttle` output.

### Validation

The updated `registration_pseudobulk()` implementation was tested against the previous `scuttle` implementation using the same example. The resulting `SingleCellExperiment` objects are now identical using:

`testthat::expect_identical(sce_pseudo, test_pseudo)` and `testthat::expect_equal(sce_pseudo, test_pseudo)`.

@Nick-Eagles and @lahuuki helped to test this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26e7f0294d03`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.