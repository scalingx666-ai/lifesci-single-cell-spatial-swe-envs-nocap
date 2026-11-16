# Issue

**Title:** Unpin numba-cuda for the RAPIDS prerelease env

## Description

The prerelease job fails at dependency resolution: `nvforest-cu13` nightlies need `cuda-core>=1`, while the `numba-cuda<0.30` pin only allows versions requiring `cuda-core<1`. Drop the pin for `rapids_prerelease` (numba-cuda 0.30.x allows `cuda-core<2`); `dev` keeps it.

Not verified end to end; the next prerelease CI run will confirm.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90bd51315c1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.