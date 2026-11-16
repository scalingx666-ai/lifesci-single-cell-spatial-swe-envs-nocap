# Issue

**Title:** Openslide backend sorting scales fix

## Description

In case a wsi has more than 10 levels then the image keys are ordered as: `['0', '1', '10', '2', ...]` when using the `.keys()` function. If a DataTree is initialized with this order the the multiscale image initializtion fails. This patch is sorting the scales for the DataTree generation correctly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10bf4a558866`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.