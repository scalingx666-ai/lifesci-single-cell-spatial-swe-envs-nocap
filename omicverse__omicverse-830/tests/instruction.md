# Issue

**Title:** fix(pl): handle COSG dotplot marker lengths

## Description

Summary:
- Handle COSG rank_genes_groups-like results where marker columns are top-N but p-value columns may be full-length.
- Align dotplot marker selection to the names column instead of silently pairing incompatible statistic lengths.
- Preserve clear errors for malformed results without a names column.

Validation:
- Verified a COSG-like result with names/scores/logfoldchanges length 50 and pvals/pvals_adj length 78 returns the expected top-marker table.
- Verified malformed results without names still raise a clear ValueError.
- Ran git diff --check.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbca54e27e24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.