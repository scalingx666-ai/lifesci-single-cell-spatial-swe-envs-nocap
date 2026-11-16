# Issue

**Title:** Defer definition of CSS classes until we know the Panels.

## Description

This aims to make it easier to write landing pages without also specifying the universe of panels twice (i.e., once in the landing page's `FUN`, and again in the initial call to `iSEE()`).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `953926a84e83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.