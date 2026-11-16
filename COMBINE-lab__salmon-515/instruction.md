# Issue

**Title:** Code for producing gibbs samples

## Description

Implementing a simple Gibbs sampler within Alevin to accept the option `--numCellGibbsSamples` and produce the `mean`, `variance`, and Gibbs estimates in the same format as of `--numCellBootstraps`.

The default `thinning factor` is set to be `16`. 

Additionally, we add `--dumpCellEq` to dump the deduplicated gene-level equivalence classes per cell.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c1bbdb4cc10e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.