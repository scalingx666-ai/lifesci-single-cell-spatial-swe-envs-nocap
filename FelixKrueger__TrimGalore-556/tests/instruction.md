# Issue

**Title:** fix(cli): reject NaN, infinite and negative -e / --max_n values

## Description

## Problem

`Cli::validate` checked the error rate with `self.error_rate < 0.0 || self.error_rate > 1.0`. Every comparison with NaN is false, so `-e nan` passed. Nothing checked `--max_n` at all.

- `-e nan` and `--max_n nan` ran the whole trim, then failed and left a half-written JSON report.
- `--max_n=-1` wrote 0 reads and exited 0.

## Fix

In `Cli::validate` (`src/cli.rs`), before any output is created:

- error rate: `!(0.0..=1.0).contains(&self.error_rate)` (rejects NaN; same message as before).
- `--max_n`: reject a value that is negative or not finite (`nan`, `inf`, `-1`) with `--max_n must be a non-negative number, got <v>`.

Valid values (`-e 0`, `-e 1`, `--max_n 0`, `--max_n 0.5`, integer counts) are unchanged.

## Testing

- New unit test `cli::tests::test_validate_rejects_nan_and_negative_float_options`: rejects `-e nan`, `-e 1.5`, `--max_n nan`, `--max_n=-1`, `--max_n inf`; accepts `-e 0`, `-e 1`, `--max_n 0`, `--max_n 0.5`. It fails without the fix (`-e nan` is accepted).
- `cargo test`: all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output change. Only invalid invocations that previously ran are now rejected up front.

## Suggested CHANGELOG entry

- **`-e` and `--max_n` now reject NaN, infinite and negative values.** `-e nan` slipped past the
  range check and `--max_n` had none, so `-e nan` / `--max_n nan` trimmed the whole file before
  failing with a half-written JSON report, and `--max_n=-1` silently wrote no reads. Both are now
  refused before any output is created.

Part of #546 (finding 9 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c98c98b56b96`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.