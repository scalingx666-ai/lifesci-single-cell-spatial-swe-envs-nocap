# Issue

**Title:** fix: boundary panics and overflow in barcode utils, knee finding and PUG edges

## Description

Adapted from #199 (thanks @IgnatiusPang). It keeps only the changes that fix a crash or a wrong result. **Output for every valid input is unchanged**, and no work is added to hot paths.

## Changes

- **`utils.rs`: barcode reference functions.**
  - 32-base barcodes computed `2^64` in the bound check. That's an overflow panic in debug; in release it wraps to 0 and the assert fails. The bound is now `4^L − 1`, computed without overflow.
  - Zero-length barcodes no longer underflow a capacity computation.
  - `get_bit_mask(0, …)` now fails with a clear message instead of shifting by a wrapped amount.
  - These functions are reference implementations: only tests call them. Production barcode correction lives in `barcode_correction.rs`.
- **`knee_finding.rs`: convergence loop.** It tested `max_idx - prev_max != 0`, which underflows when the knee moves *down* between iterations. That happens on real data: 4748 → 4661 → 4645 on a chromium v3 run. Debug builds panicked; release builds wrapped, which is exactly `!=`. The loop now tests `max_idx != prev_max`, so release output is unchanged.
- **`pugutils.rs`: one-edit edge direction.** The test `x > 2y − 1` moves into an inlined helper that computes `x ≥ 2y` in u64. For counts ≥ 1 the two are identical; a test checks this exhaustively against the historical rule. The u64 form can't underflow at `y = 0` or overflow at `y > 2^31`. There's no extra Hamming-distance computation in the pairwise loop.

## Not taken from #199

- **The knee slice bound change (`len-1` → `len`).** It isn't needed for any of the fixes, and it changed the chosen knee on about 1.6% of 20,000 synthetic histograms, off by 1–9. That's a silent change to `generate-permit-list -k` output.
- **Early returns in knee finding.** For 1–2 barcodes or all-zero input they returned a knee of 0 or 1. Develop instead stops with an explicit "check the mapping rate" error, which is kept.
- **A helper that recomputed the Hamming distance** for every two-way edge in the O(n²) UMI-graph loop.

## Validation

- **Tests:** they pass in debug and release (78 library tests plus the integration suites), and clippy and fmt are clean. The 4 new regression tests fail on develop.
- **chromium v3, 5M reads:** the knee permit list is identical (4,646 cells, same correction statistics), and the parsimony quant matrix is canonically identical to develop's (2,770,761 nonzero entries).
- **3 GB long-read RAD, parsimony, 16 threads, 3 alternating runs:**

  | | wall time (s) | peak memory |
  |---|---|---|
  | develop | 2.38, 2.38, 2.38 | 866–899 MB |
  | this branch | 2.39, 2.37, 2.36 | 880–917 MB |

  The output is canonically identical (15,541,130 nonzero entries).

Supersedes #199.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Xg1hUw9i95rJikA6eL2WNH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da199c923e2e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.