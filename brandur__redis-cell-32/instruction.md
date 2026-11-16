# Issue

**Title:** Remove Clippy from nightly builds

## Description

Clippy is only available intermittently in nightly builds, and isn't
available right now which is breaking the build. Here we disable it for
nightly builds.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `59b3fd477157`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.