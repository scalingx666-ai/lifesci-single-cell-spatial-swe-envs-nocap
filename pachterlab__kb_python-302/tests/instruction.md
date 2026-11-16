# Issue

**Title:** Add --cellranger, --gzip, --delete-bus, and --genomebam/--cram support

## Description

Implements GitHub issues #295 and #296:

Issue #295: CellRanger-compatible output
- Added --cellranger flag that auto-enables gzip compression
- For nac/lamanno workflows, automatically creates spliced/ and unspliced/ subdirectories
- Output format compatible with Seurat's Read10X() function
- Gene symbols output in GENE_ID\tGENE_SYMBOL format

Issue #296: Disk space optimization
- Added --gzip flag for manual gzip compression control
- Added --no-gzip flag to disable auto-compression with --cellranger
- Added --delete-bus flag to remove intermediate BUS files after successful count
- Compressed output reduces file sizes by 70-90%

Additional features:
- Re-enabled --genomebam flag for BAM output (previously hidden)
- Added --cram flag for CRAM format support (requires --genomebam)

Changes:
- Modified matrix_to_cellranger() to support gzip compression
- Updated count(), count_nac(), and filter_with_bustools() with new parameters
- Auto-enable logic: --cellranger automatically enables gzip and cellranger-style directories
- BUS cleanup logic deletes intermediate files only after successful completion

Backward compatible: All changes use optional parameters with defaults maintaining existing behavior

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dadae35cd8f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.