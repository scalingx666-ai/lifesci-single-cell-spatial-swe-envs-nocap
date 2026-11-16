# Issue

**Title:** Fix compatibility with {anndata}

## Description

This is a proposed solution for #75. This ensures that no implicit `py_to_r(...)` conversion occurs in `AnnDataToSCE(...)` using the `disable_conversion_scope(...)` helper function stolen from reticulate :)).

* All values extracted from the AnnData objects (e.g. `adata$X`) need to manually converted to an R object.
* If an AnnDataR6 is passed to AnnData2SCE, it first gets converted to a Python AnnData.
* `{anndata}` was added to `Suggests:` so it can be tested during the unit tests. However, I think it'd be better to move the `library(anndata)` call to a lower point in the unit test. @lazappi WDYT?

I apologise for the many commits; I couldn't install rhdf5 so I had to use the CI for running the full R CMD Check. If this PR gets accepted at some point, I think it makes sense to squash.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4943d3a8ff06`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.