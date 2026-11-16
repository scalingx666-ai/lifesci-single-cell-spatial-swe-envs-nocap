# Issue

**Title:** Deterministic shared barcode correction for RNA and Flex

## Description

Implements the shared barcode-correction architecture for ordinary and multi-sample RNA. Depends on libradicl PR #56.

Highlights:
- central deterministic Hamming-1 / substitution-or-shift-1 engine with Unique and exact-rational Frequency policies
- all RNA filter modes share frozen-prior correction and aggregate corrected permit frequencies
- Exact, Unique, and Frequency sample correction, including one-pass bounded Snappy spill/replay for structurally ambiguous sample/cell pairs
- versioned correction_plan.bin handoff; collation applies compiled decisions directly and retains legacy fallbacks
- deterministic ordering, preserved legacy permit artifacts and sample_info meanings, explicit collatable_reads diagnostics
- deprecated sample 1-edit interface remains compatible

Validation:
- release all-target test suite and clippy with warnings denied pass
- correction plans invariant to whitelist ordering and thread count; malformed/trailing artifacts error
- full 39.9 GB Flex GPL median: 31.32 s vs 32.21 s baseline, RSS 1.78 GB vs 2.58 GB
- full Flex collate median: 21.92 s vs 24.50 s, RSS 1.24 GB vs 1.30 GB
- 2.6 GB single GPL median: 2.25 s vs 2.26 s, RSS 328 MiB vs 357 MiB
- single collate median: 1.65 s vs 1.77 s, RSS 897 MiB vs 907 MiB

ATAC integration and the detailed documentation/measurement report are intentionally split into follow-up stacked PRs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7fee4624b378`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.