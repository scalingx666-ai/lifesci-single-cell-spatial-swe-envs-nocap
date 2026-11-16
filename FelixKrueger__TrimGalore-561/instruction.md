# Issue

**Title:** fix(report): count only too-short pairs on the PE length-cutoff line

## Description

## Problem

The paired-end text report prints `pairs_removed` under the label "Number of sequence pairs removed because at least one read was shorter than the length cutoff". That counter also includes pairs dropped for N content, `--max_length` and `--discard_untrimmed`.

```
trim_galore --paired --max_length 60 --discard_untrimmed \
  test_files/BS-seq_10K_R1.fastq.gz test_files/BS-seq_10K_R2.fastq.gz
```

prints 9,997 (99.97%) on that line. Only 4 pairs were too short; 6,841 were too long and 3,152 were discarded as untrimmed (the JSON and the per-read RUN STATISTICS lines already say so).

Perl 0.6.11 counts only length-cutoff removals in `$sequence_pairs_removed` (`trim_galore` ~2285-2324); N-content and too-long removals are separate counters.

## Fix

- New `PairValidationStats::pairs_removed_too_short`, next to the existing `pairs_removed_too_long`, merged like the others.
- Incremented in the three `PairFilterResult::TooShort` arms (serial FASTQ loop, uBAM-output loop in `trimmer.rs`, `classify_paired` in `parallel.rs`).
- `write_pair_validation_stats` prints it on the "shorter" line. Wording and line shape are unchanged.

No new lines were added: too-long removals ("Sequences removed because they were longer than the upper length cutoff") and untrimmed discards ("Reads discarded as untrimmed") are already in the same report. `pairs_removed` is unchanged and still feeds the JSON and the stderr "Pairs removed" total.

## Testing

- New `tests/integration_pe_report_removed.rs::pe_report_shorter_line_counts_only_length_removals`: four hand-made pairs (one passes, one too short, one without adapter, one too long), run with `--max_length 60 --discard_untrimmed` at `--cores 1` and `--cores 2`. Expects `1` (25.00%) on the line.
- Without the fix the test fails: `--cores 1` printed 3 (75.00%). With the `parallel.rs` increment removed, `--cores 2` printed 0, so both counting paths are covered. The uBAM-output arm is not covered by the test.
- `cargo test`: all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.
- Repro above now prints 4 (0.04%).

## Byte-identity

With default flags no pair is removed for N, length-above-max or missing adapter, so the new counter equals `pairs_removed` and the report is unchanged (BS-seq_10K default run: 4 on the line, 4 in "Pairs removed"). No trimmed FASTQ output changes.

## Suggested CHANGELOG entry

- **The paired-end "shorter than the length cutoff" line now counts only too-short pairs.** It used to show every removed pair, including those dropped for N content, `--max_length` and `--discard_untrimmed`; a BS-seq run with `--max_length 60 --discard_untrimmed` reported 9,997 "too short" pairs where only 4 were. The other removals already have their own lines in the report.

Part of #546 (finding 5 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82b64d99c4dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.