# Issue

**Title:** [r] Add examples for Genomic Range Calculations

## Description

Provides examples for the genomic range calculations examples.  I've noticed `normalize_ranges()` was not exported, so also exported that as well.  

The example for `gene_score_tiles_archr()` just uses the basic gencode genes.  Additionally, the number of rows outputted is dependent on the tile width of the function.  This current output has around 6 million rows.  Should we try to cut this down?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16faeade0a26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.