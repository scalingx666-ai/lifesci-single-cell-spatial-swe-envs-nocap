# Issue

**Title:** Handle NaNs in nextflow export

## Description

NaNs are not correctly parsed by netlify. This converts non-finite metric outputs to strings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `372f8c7d1275`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.