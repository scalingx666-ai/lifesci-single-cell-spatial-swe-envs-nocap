# Issue

**Title:** Feature/split abs times

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Add :meth:`cellrank.estimators.GPCCA.compute_absorption_times` to compute mean and variance of the time to absorption.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
Adjusted previous tests.

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2fe5777ed876`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.