# Issue

**Title:** Save gene sets without cell annotations

## Description

This fixes a bug whereby new gene sets csv files created without accompanying cell-level annotations could not be detected by the filecrawler. Previously, the filecrawler only displayed csv files corresponding to cell-level annotations. This meant that if the user created a new gene set but no cell-level annotations then, whilst the gene-set csv would be saved, they could not be loaded from filecrawler.

Note; this commit also changes the behaviour when checking whether a file is a gene set. It now checks whether the file extension is `self.gene_set_file_suffix` (by default, `_gene_sets.csv`). This means that patterns such as `foo_gene_sets_bar.csv` will no longer count as a gene_sets file. I made this change for convenience here, but obviously please revert if you are worried that it will break things - it just seemed cleaner this way.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d10932b0690`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.