# Issue

**Title:** Fix/aggregate_absorption_probabilities violin

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Fix cluster subsetting in :func:`cellrank.pl.aggregate_absorption_probabilities` and ``mode = 'violin'``.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
1 new test.

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5853d0e0c48c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.