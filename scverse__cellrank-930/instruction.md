# Issue

**Title:** Lift restriction on projection, allow passing conn

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Allow passing connectivities for transition matrix projection. Useful when the kernel is not kNN-based.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
1 new test, modified existing tests.

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f1fbdd750d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.