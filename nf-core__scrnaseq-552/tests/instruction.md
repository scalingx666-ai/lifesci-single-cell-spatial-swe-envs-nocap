# Issue

**Title:** Star igenomes compatibility

## Description

The STAR indices that we provide in the `igenomes.config` are all incompatible with the STAR version we ship in the pipeline. However, the incompatibilities are purely symbolic, and small modifications are sufficient to make them compatible. nf-core/rnaseq found a solution for how this can be done. This PR adds the same solution to nf-core/scrnaseq. As there is no official nf-core module for this yet, I copied the local module from rnaseq to scrnaseq.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e8070df6809e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.