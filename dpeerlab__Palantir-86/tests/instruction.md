# Issue

**Title:** added seed option

## Description

These code edits allow to get identical results when re-running function `palantir.utils.run_diffusion_maps`. The solution is to fix the Numpy random seed before calling function `scipy.linalg.eigs`. If the seed option is unspecified (default) then then seed is reset to a random state.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9de2ce1a8475`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.