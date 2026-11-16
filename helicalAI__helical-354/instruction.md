# Issue

**Title:** Nicheformer: ENSEMBL and attn maps

## Description

We are adding:
1. Conversion of gene IDs to ENSEMBL - #352
2. Facilities for attention map extraction - #353

We are bumping a dependency version:
black 26.1.0 -> 26.3.1

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e43e01609e7d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.