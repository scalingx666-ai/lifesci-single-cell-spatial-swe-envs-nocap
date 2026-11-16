# Issue

**Title:** Merge devel into master

## Description

### `count`
- Fixed `loompy does not accept empty matrices as data` error when providing `--loom` with `--workflow lamanno` (#91)
- When using `--h5ad` or `--loom` with `-x smartseq`, the output matrix has genes as columns, instead of transcripts. For genes that have multiple transcripts, the counts are added. (#93)
- For `-x smartseq`, it is now possible to provide a batch TSV instead of FASTQs directly. The batch TSV must contain exactly three columns: cell ID, FASTQ 1 (read 1), FASTQ 2 (read 2).
- Added an error when an uneven number of FASTQs are provided for `-x smartseq` (only paired-end reads are currently supported)
- Turned off all logging and warning messages from `h5py` and `anndata`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b997e0d469fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.