# Issue

**Title:** Compute 20 Schur vectors by default

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Fix not being able to use ``minChi`` in :meth:`cellrank.estimators.GPCCA.fit`. Also compute 20 Schur vectors by default.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
N/A

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9452dc14eb68`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.