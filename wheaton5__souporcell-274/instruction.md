# Issue

**Title:** singularity and souporcell_pipeline.py update

## Description

Added version to souporcell_pipeline.py
Check executable availability before running (.py, souporcell, and troublet)
Warning for raw barcodes (>200,000 barcodes)
Recommend using souporcell3 with khm for k > 16 in both .rs and pipeline
.def updated

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7ecc474d124`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.