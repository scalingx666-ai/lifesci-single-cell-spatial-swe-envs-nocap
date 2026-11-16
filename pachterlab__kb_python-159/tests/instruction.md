# Issue

**Title:** merge devel into master

## Description

### General
* **[DEPRECATION]** Support for split indices (with the `-n` option) will be deprecated in the next major release. It is now recommended to use `--include-attribute` and `--exclude-attribute` options, similar to Cellranger's `mkref` options (https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/advanced/references), to `kb ref` to reduce index size and memory usage.

### `ref`
* A remote URL may be provided as the `fasta` (genomic FASTA) and/or `gtf` (gene annotation GTF) arguments. Support from `ngs_tools 1.5.13`.
* GTF is now allowed to have 0-length segments ().

### `count`
* **[DEPRECATION]** Technology `SMARTSEQ` is now deprecated. All future uses should use `BULK`, `SMARTSEQ2` or `SMARTSEQ3`.
* Genes that do not have a gene name will now have their gene IDs in the `gene_name` column (or the `adata.var_names` if `--gene-names` is used).
* Support for `--workflow lamanno` for `-x BULK` and `-x SMARTSEQ2` technologies.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f5e2cd07de8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.