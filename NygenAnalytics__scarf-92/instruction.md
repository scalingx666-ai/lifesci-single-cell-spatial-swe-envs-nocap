# Issue

**Title:** Added HTO demultiplexing feature

## Description

Added `mark_hto_identities` method in `DataStore` which performs HTO demultiplexing using Seurat's HTODemux function

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a2742845fe5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.