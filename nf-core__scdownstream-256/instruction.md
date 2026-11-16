# Issue

**Title:** Fix SingleR obs naming

## Description

This PR fixes an issue with SingleR, where individual sample names were added to the obs names and thus cannot be merged downstream, losing the cell type data therein.

## PR checklist

- [X] This comment contains a description of changes (with reason).
- [X] Make sure your code lints (`nf-core pipelines lint`).
- [X] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16160a5dc73d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.