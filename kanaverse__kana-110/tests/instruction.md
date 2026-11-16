# Issue

**Title:** Adding block-awareness to all relevant steps.

## Description

Untested. 

This requires formulation of the batch vector in `_inputs.js`. This should be an `Int32WasmArray`, so best to use `allocateCachedArray` of length equal to the total number of columns across all samples.

I'll need another UI element at the PCA step asking for "none", "mnn" or "regress" - this should be passed in as `block_method` in the `compute()` function of `_pca.js`, at around L85 of `scran.worker.js`. (Might as well do the reverse in L222.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `721fece847e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.