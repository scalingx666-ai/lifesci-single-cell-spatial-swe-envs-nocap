# Issue

**Title:** Fixes to ensure back-compatibility.

## Description

I accidentally pushed 4f4bcc7a479e15b89e21a565e3067efd8a82fb86 to `master` (not sure why I had permissions to do so) so this PR is to fix all the problems to make it _actually_ merge-ready.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f4bcc7a479e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.