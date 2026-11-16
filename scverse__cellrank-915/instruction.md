# Issue

**Title:** Fix/precomputed kernel adata

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Fix using sentinel value when using :class:`cellrank.kernels.PrecomputedKernel.` and neither key nor direction was specified.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
1 new parametrized test.

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->
cloes #906

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb182f5a2cdc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.