# Issue

**Title:** Remove numpy/scipy monkey-patches, bump pygam>=0.9

## Description

The monkey-patches in __init__.py were workarounds for pygam < 0.9:
- sp.spmatrix.A: pygam used .A (deprecated scipy alias for .toarray())
- np.int = int: pygam used np.int (removed in numpy 2.0)

Both are fixed in pygam >= 0.9. Remove the patches and bump the lower bound from 0.8 to 0.9.

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `128c05bbb108`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.