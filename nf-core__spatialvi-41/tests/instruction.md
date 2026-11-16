# Issue

**Title:** Manual alignment in samplesheets

## Description

This PR adds functionality to specify manual alignment files in the samplesheets rather than via a parameter. In addition to this, the samplesheet checker has been updated to conform to the latest nf-core template, which meant major changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `753bdd5fe660`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.