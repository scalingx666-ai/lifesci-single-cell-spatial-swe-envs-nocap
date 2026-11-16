# Issue

**Title:** Fix Clippy (lint) warnings and add Clippy to CI

## Description

Fixes various issues that were exposed by running Clippy against the
codebase and adds Clippy to CI so that future pull requests will be
checked for problems automatically.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cce0c2f9211d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.