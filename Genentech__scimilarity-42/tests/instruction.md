# Issue

**Title:** Change: formatted and reconfigured zarr imports for zarr 3

## Description

Hey, 

I changed how imports of zarr classes are handled to support Zarr 3.

I also added some non-runtime imports across modules so that your future annotations work as intended.

Finally, I ran some default ruff formatting + checks over the repo.

Cheers,

Max H.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc3fb555dea7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.