# Issue

**Title:** fix(demux): sort tied summary rows by barcode

## Description

## Problem

`<base>_demultiplexing_summary.txt` (and the matching stderr block) sorts rows by count only. The counts are in a `HashMap`, so rows with equal counts come out in hash order, which differs per process. Barcodes with zero reads are common, so two identical runs gave summary files with different md5s.

Perl 0.6.11 does the same: `sort { $barcode_counts{$b} <=> $barcode_counts{$a} } keys %barcode_counts`, and Perl's hash key order is randomised per process. There is no defined Perl order for ties to match.

## Fix

Tie-break on the barcode: `b.1.cmp(a.1).then_with(|| a.0.cmp(b.0))`. `NoCode` is a key in the same map and sorts with the barcodes by plain string order.

## Testing

- New unit test `demux::tests::test_demultiplex_summary_ties_sort_by_barcode`: 8 barcodes, one read for `TTTT`, one unmatched read, and the expected 9 rows written out by hand (`NoCode` and `TTTT` tie at 1, then 7 barcodes tie at 0). With the tie-break removed it failed in 3 of 3 runs; with it, it passes.
- `cargo test`: all suites pass (846 tests).
- `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

Only the order of tied rows in the summary file and the stderr summary changes. The CI demux validation compares the four `.fq.gz` outputs, not the summary file, so it is unaffected. FASTQ outputs are unchanged.

## Suggested CHANGELOG entry

- **The `--demux` summary file is now the same across identical runs.** Rows with equal counts were
  printed in hash order, so two identical runs could write different files. Ties now sort by
  barcode.

Part of #546 (finding 20 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c98c98b56b96`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.