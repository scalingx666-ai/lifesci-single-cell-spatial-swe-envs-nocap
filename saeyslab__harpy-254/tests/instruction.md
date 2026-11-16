# Issue

**Title:** Fix typo and type annotation in xenium reader API

## Description

There was a small typo in one of the parameters of `hp.io.xenium()`: `morpholohy_focus` instead of `morphology_focus`. And the type annotation for `filter_gene_names` did not specify `None` as a possibility.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0db802fb9be`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.