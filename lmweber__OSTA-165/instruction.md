# Issue

**Title:** Merge sandbox into devel

## Description

Merge `sandbox` into `devel` branch for a public build.

Includes Visium HD workflow contributed by @estellad and @HelenaLC (among other things).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df54f0ef02ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.