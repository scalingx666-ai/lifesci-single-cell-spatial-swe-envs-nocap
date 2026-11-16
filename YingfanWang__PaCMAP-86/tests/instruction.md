# Issue

**Title:** provide override; fixes #84

## Description

by setting `PACMAP_DISABLE_CHECKS=1` (or `true` or `yes) in one's environment, this change allows the user to opt-out of the checks to the number of neighbors and far points (bringing back behavior from `pacmap==0.7.3`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `904d863fb780`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.