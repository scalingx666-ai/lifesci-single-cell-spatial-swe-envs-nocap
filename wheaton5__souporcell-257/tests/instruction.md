# Issue

**Title:** Feat: Add souporcell3

## Description

Changes to README to include information about Souporcell3.
params.yml updated to include two parameters: souporcell3 and clustering_method.
With souporcell3 set to true, bad cluster detection is activated and runs three times if bad clusters are detected. Default is false.
Changing clustering_method to khm uses khm for clustering. Default is em.
Warnings fixed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `08d3c2ef34a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.