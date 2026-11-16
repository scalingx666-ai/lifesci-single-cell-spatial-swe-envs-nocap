# Issue

**Title:** Add `uwot::umap2` support

## Description

Hi Seurat Team (@AtSourav)

This PR implements changes 1 and 3 mentioned in #9709.

1. It allows for users to pass `umap.method = "uwot2"` which will implement `uwot::umap2`.  No changes made to parameters that are passed to `umap2` just added as additional method.  
2. It removes old warning that uwot does not support `metric = correlation` since it now does support that.
3. Updated manual entry to remove mention of `method = uwot-learn` since that was deprecated and no longer exists (warning already present in code if user supplies it) and replaces it with entry for `umap.method = "uwot2"`.

If there are any other changes you think should be made or updates I need to make please let me know.

Thanks as always!
Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5d9535493fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.