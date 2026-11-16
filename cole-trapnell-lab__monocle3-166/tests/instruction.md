# Issue

**Title:** DESCRIPTION is missing ggrastr remote

## Description

Hi @ctrapnell, I noticed that monocle3 currently doesn't install clean without the [ggrastr](https://github.com/VPetukhov/ggrastr) remote specified, since that package isn't on CRAN.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0a508e1a6bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.