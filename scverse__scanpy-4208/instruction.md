# Issue

**Title:** fix: PCA centering in ingest

## Description

Ingest centers its PCA against the query data not the fit data. I also made PCA sparse

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fde258b0c756`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.