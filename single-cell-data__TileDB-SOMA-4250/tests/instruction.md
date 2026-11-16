# Issue

**Title:** Supporting X missing/None for EAQ to_anndata

## Description

**Issue and/or context:**

`X_layer_name` is an optional parameter on `tiledbsoma.io.to_anndata()`, allowing users to create anndata objects where `X` is empty.

We should make exporting X optional for `tiledbsoma.ExperimentAxisQuery.to_anndata()` as well, currently it's a required parameter.

**Changes:**

- Chaning EAQ.to_anndata function to support the optional X in parity with `tiledbsoma.io.to_anndata`
- Adding unit test for the support of optional X for EAQ API

**Notes for Reviewer:**

- In our tests we don't include comparisons against the extra `soma_joinid` column that is being produced by the EAQ API but not from the soma.io.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f53e34391b0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.