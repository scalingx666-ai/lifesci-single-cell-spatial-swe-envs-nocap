# Issue

**Title:** Add omp library to the runtime image

## Description

# Description

This PR adds the `libgomp1` package to the runtime build. Without this, STAR did not start due to `STAR: error while loading shared libraries: libgomp.so.1`. 

Another minor change is the removal of `gcc` from the build stage, since the compiler is already part of `build_essential`.

## Type of change

Please delete options that are not relevant.

- [x] Bug fix (non-breaking change which fixes an issue)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d39f2434550`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.