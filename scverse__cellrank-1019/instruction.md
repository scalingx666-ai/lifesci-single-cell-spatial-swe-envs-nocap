# Issue

**Title:** Fix/cytotrace anndata save

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Fix not being able to save :class:`~anndata.AnnData` after :class:`~cellrank.kernels.CytoTRACEKernel` was run.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
No new tests.

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d7f499c019d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.