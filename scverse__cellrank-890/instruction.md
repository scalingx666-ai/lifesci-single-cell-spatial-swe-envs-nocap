# Issue

**Title:** Add argument `subset_to_serum`

## Description

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->

Add argument ``subset_to_serum`` to :func:`cellrank.datasets.reprogramming_schiebinger` to allow downloading the subsetted data. This includes the transition matrix computed with the :class:`cellrank.external.WOTKernel`.

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->
.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8761040096e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.