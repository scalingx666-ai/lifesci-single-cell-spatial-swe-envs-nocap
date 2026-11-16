# Issue

**Title:** Python Version Check

## Description

Hi @FelixKrueger,

I ran some tests on the updated master branch and both single-core and multi-core seem to be working as expected with both Python 2 and Python 3 environments. I did find a small difference in how Python outputed its version so I created this pull request to solve the problem. I also ran a couple single-end tests that also seem to be working as expected.

Thanks, Frankie

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7d4dc7c6c5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.