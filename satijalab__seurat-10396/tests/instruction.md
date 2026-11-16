# Issue

**Title:** Add sanity check for two layers needed for IntegrateLayers

## Description

Taking the suggestion from issue #9381 on including a sanity check for at least 2-layers in the input for IntegrateLayers() function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83f9659912bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.