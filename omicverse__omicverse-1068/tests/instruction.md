# Issue

**Title:** ov.read: back to storage='memory' by default

## Description

Reverts the default from #1067: several functions (ov.single.get_celltype_marker, sc.tl.rank_genes_groups, ...) raise on the disk-backed AnnDataOOM. anndataoom + dask stay dependencies for storage='disk'; a compatibility audit follows.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b085595aadb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.