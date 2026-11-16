# Issue

**Title:** WSI processing updates

## Description

Here is a PR for the WSI processing folks. The changes introduced are:

- The functions and classes have been renamed to follow the new API organization `sopa.patches` instead of `sopa.embedding`
- The inference function now accepts a callable object with arbitrary output dimension
- Patch processing with overlaps is now allowed
- Corresponding doc updates

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f80174693d4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.