# Issue

**Title:** Rustfmt and Clippy are now available on the stable channel

## Description

The build is currently broken because the method I was using to install
Rustfmt and Clippy is no longer working. Both these programs are now
available as stable components, so change the Travis sequence to take
advantage of that (and fix the build).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `456f0b5f5ad2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.