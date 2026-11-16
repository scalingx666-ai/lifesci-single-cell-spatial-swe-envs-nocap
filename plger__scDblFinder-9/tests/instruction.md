# Issue

**Title:** Migration of scran doublet functions: part 1

## Description

## Overview

This begins what I promised to do in our offline conversations. I've started with a relatively simple function that recovers intra-sample doublets from multiplexed datasets where the inter-sample doublets are known. You can see it in action [here](https://osca.bioconductor.org/doublet-detection.html#guilt-by-association-for-unmarked-doublets), though the current PR has renamed it to `recoverDoublets`, which is a nicer name.

The function itself is pretty simple, and you can see some of the theoretical reasoning in its documentation.

## Points of interest

- Added tests for `recoverDoublets` via **testthat**.
- `recoverDoublets` uses a neat S4 dispatch mechanism that allows it to work on matrices, SEs and SCEs.
- Switched several imports from **scater** to **scuttle**, a lower-level utility package.
- Removed the general `import(Matrix)` in favor of more targeted `importFrom` statements, this should not break anything AFAICT but we should keep an eye out for problems.
- I took the liberty of adding myself as a contributor in the author list.

## Further comments

I forgot to mention in the docs that the behavior of this function is conditional on the existing distribution of inter-sample doublets. For example, when two or more cell types are unique to a sample, their inter-sample doublets will not be detected with hashing approaches, and thus the inter-sample doublets will also not be detected.

Conversely, the reasoning used to derive X only makes sense for replicate samples. If people multiplex together samples that are hugely different, X should be an overestimate and too many cells will be removed. Which is not too bad, just a bit conservative. Should mention this in the documentation under "Caveats" or something.

If you wanted, you could probably do something with the identity of the two samples in each doublet, e.g., to estimate each sample's proclivity to form doublets and use that to weight the proportions. Dunno if that's worth it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `72a3cb789a15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.