# Issue

**Title:** Develop

## Description

Merge develop into main.  This addresses #114 (which was a unmaintained dependency used by one of `alevin-fry`'s dependencies).  This also takes the opportunity to update other outdated packages, which also required updating and bumping `sce` and `libradicl`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73e3af6ebd7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.