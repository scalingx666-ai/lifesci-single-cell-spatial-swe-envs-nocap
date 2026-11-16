# Issue

**Title:** Fix None in ligrec source/target

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Fix source/target being ``None`` in :func:`squidpy.gr.ligrec`.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
1 new test.

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cae246a9fa5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.