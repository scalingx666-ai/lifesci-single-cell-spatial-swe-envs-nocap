# Issue

**Title:** perf: drop per-read allocations in the adapter DP and 5' clip

## Description

## Problem

Two allocations sit on the per-read hot path:

- `alignment::find_3prime_adapter` built its DP table as `vec![vec![0; n + 1]; m + 1]`: `m + 1` heap allocations (14 for the 13 bp Illumina adapter) for every read that passes the Myers prefilter.
- `FastqRecord::clip_5prime` built three `String`s per clipped read: the clipped prefix, plus new copies of the remaining sequence and quality. It runs on every read under `--clip_R1` / `--clip_R2`, and on every R2 under RRBS paired-end. Only `--rename` uses the clipped prefix.

## Change

- The DP table is one flat `Vec<usize>` with row stride `w = n + 1`. The fill loop takes the previous and current rows as slices (`split_at_mut`). The read-only scans and `backtrace_start` index it as `i * w + j`. `backtrace_start` now takes `(&[usize], w)` instead of `&[Vec<usize>]`.
- `clip_5prime` `drain`s sequence and quality in place and returns `bool` (whether it clipped) instead of `Option<String>`. The only caller that used the string, `--rename` in `trimmer::apply_trimming`'s clip step, now copies the prefix before clipping, the same way `specialty.rs` already did. The other four callers ignored the return value. `clip_3prime` is unchanged: it already truncates in place and only allocates the clipped suffix.

## Timing

Input: `test_files/illumina_10K.fastq.gz` concatenated 50 times (500K reads), serial, `hyperfine -N`, Apple Silicon laptop.

| | before | after |
|---|---|---|
| `--clip_R1 5` (8 runs) | 2.55 s ± 0.06 | 2.01 s ± 0.02 |
| default flags (6 runs) | 2.59 s ± 0.05 | 2.01 s ± 0.02 |

Almost all of the gain comes from the DP fill loop. Built alone, the `clip_5prime` change was within noise (2.60 s ± 0.12 vs 2.54 s ± 0.03). A first version of the flat table that indexed `dp[i * w + j]` inside the fill loop too was about 10% *slower* than before. The speed-up comes from the row slices in the inner loop, not from merging the allocations.

## Testing

Behaviour must not change, so the existing tests are the guard: the 20 unit tests in `src/alignment.rs` (including `myers_no_false_negatives_against_scalar_dp`, which compares the prefilter against this DP), `test_fastq_record_clip_5prime` / `test_fastq_record_clip_too_short` (updated for the `bool` return), and the `--rename` `:clip5:` assertions in `tests/integration_ubam_out.rs`.

I also compared the old and new binaries' decompressed outputs (md5) and trimming reports (`diff`). They were identical for SE default, `--clip_R1 5 --three_prime_clip_R1 3`, the same with `--rename`, RRBS PE, RRBS non-directional, `--poly_a`, PE `--cores 4 --clip_R2 3`, `--hardtrim5 30 --rename`, Nextera, smallRNA, multi-adapter `file:` input, and the 500K-read input.

`cargo test`: all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output byte changes; see the comparisons above.

## Suggested CHANGELOG entry

- **Adapter matching is about 20% faster.** The alignment DP table is now one buffer filled through row slices instead of one `Vec` per row, and the 5' clip (`--clip_R1/R2`, RRBS R2) trims in place instead of copying sequence and quality. Output is unchanged; on 500K Illumina reads a serial run went from 2.55 s to 2.01 s.

Part of #546 (finding 19 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c3515a2f5f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.