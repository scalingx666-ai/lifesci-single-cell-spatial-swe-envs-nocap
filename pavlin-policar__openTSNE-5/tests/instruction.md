# Issue

**Title:** Add conda recipe

## Description

Make the package distributable with conda.

`pynndescent` is not installable with conda, which means that either I can could do that myself (which is a lot of maintaining) or I could copy the code here and distributed it with this package. While not ideal, the second option seems better.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0df498b18f41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.