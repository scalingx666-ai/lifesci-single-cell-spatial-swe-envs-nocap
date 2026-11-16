# Issue

**Title:** Update to v0.42.5

## Description

`pseudo` mode:
- A new mode `kallisto pseudo` has been implemented which allows reads to only be pseudoaligned. This mode is useful during single cell analysis as many different experiments (single cells) can be analyzed at the same time and their equivalence classes will be consistent. It will also output a matrix of equivalence class counts (as used in [Fast and accurate single-cell RNA-Seq analysis by clustering of transcript-compatibility counts](http://biorxiv.org/content/early/2016/03/04/036863)).

Bug fixes:
- Fixes a segfault when running quant in `--bias` mode
- Fixes a small error in allocation of memory
- Ensures that single-end reads have reasonable length mappings when mapping to short transcripts

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f0678a263965`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.