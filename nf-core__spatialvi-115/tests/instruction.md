# Issue

**Title:** Futureproofing

## Description

This PR makes changes according to the new Nextflow strict syntax, as well as some minor formatting and harmonisation changes.

## PR checklist

- [X] This comment contains a description of changes (with reason).
- [X] Make sure your code lints (`nf-core pipelines lint`).
- [X] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [X] `CHANGELOG.md` is updated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28b1fc0f358c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.