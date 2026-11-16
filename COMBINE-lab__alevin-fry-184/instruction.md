# Issue

**Title:** Use shared deterministic correction in ATAC

## Description

Stacked on #183.

This applies the same alevin-fry-owned correction engine and correction_plan.bin handoff to the ATAC pathway:
- ATAC GPL supports Unique or Frequency and Hamming-1 or substitution-or-shift-1
- defaults remain Hamming-1 Unique, with 90% as the resolved Frequency confidence
- observed unmatched barcodes are counted rather than stored once per read
- corrected reads are aggregated into permit_freq.bin
- both ATAC collation and genomic sorting consume the compact plan, with permit_map.bin fallback for older outputs
- barcode ties in ATAC collation are fully ordered

Tests verify the default plan and retained identities, and prove both collation and sorting work after the legacy map is removed. The full release test suite and clippy with warnings denied pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7330a59b3dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.