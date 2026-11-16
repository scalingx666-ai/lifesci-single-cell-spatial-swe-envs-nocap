# Issue

**Title:** Replace deprecated force_all_finite with ensure_all_finite

## Description

sklearn renamed force_all_finite to ensure_all_finite in 1.6 and removed the old name in 1.8. Bump minimum to scikit-learn>=1.6.0.

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6d313f062918`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.