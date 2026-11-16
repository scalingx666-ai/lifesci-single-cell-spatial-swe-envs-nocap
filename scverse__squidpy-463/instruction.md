# Issue

**Title:** Explicitly check for None in complex policy

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Finally fixes ``squidpy.gr.ligrec`` ``None`` values.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
N/A (there's already a test present).

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->
handles #443

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db64d715e6a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.