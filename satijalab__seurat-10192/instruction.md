# Issue

**Title:** Fix/dimplot data (v5.3.1)

## Description

< v5.3.1, data (metadata + dimensionality reduction embeddings) for `DimPlot` was retrieved entirely using the `FetchData` function.

In the release of v5.3.1, an update was made to address the issue of having metadata column names that conflict with dimensionality reduction embeddings. The fix was to fetch only metadata and bind the embeddings columns separately. However, `FetchData` has a different method of cleaning & retrieving data, sometimes resulting in a length mismatch when binding the two dataframes. (error: `Error in data.frame(..., check.names = FALSE) : arguments imply differing number of rows`.

This PR proposes a reversion (so that `FetchData` goes back to fetching both embeddings & metadata at once) and instead throws a warning to the user when `DimPlot` is called on data with conflicting metadata & embedding colnames.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e0ffd76cf46d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.