# Issue

**Title:** fix(cli): reject --basename in modes whose output naming ignores it

## Description

## Problem

Several output namers take no basename, so `--basename` was accepted and silently dropped:

- `--hardtrim5` / `--hardtrim3` (`specialty.rs` namers)
- `--clock` / `--implicon` (`specialty.rs` namers)
- single-file interleaved uBAM input, i.e. `--paired` with one BAM file, for both `--output-format fastq` (`InterleavedFastqOutputs`) and `--output-format ubam` (`InterleavedBamOutputs`)

Example: `trim_galore --paired --basename foo ubam_paired_test.bam` wrote `ubam_paired_test_val_1.fq` / `_val_2.fq` with no warning.

## Fix

Refuse the combination before any output is created:

- `Cli::validate` (`src/cli.rs`): `--basename` with `--hardtrim5`, `--hardtrim3`, `--clock` or `--implicon` is an error. It sits ahead of the existing multi-input `--basename` checks so this message wins.
- `main()` (`src/main.rs`): `--paired` + one input + `--basename` is an error, placed directly after the existing "single paired input must be a uBAM" guard. That check needs the detected input format, which `validate()` cannot see; it runs before `ensure_output_dir`, the pre-flights and every dispatch branch.

`--clump_only` is exempt: its interleaved namer (`clumped_paired_bam_output_name`) does honour `--basename`.

## Perl 0.6.11

Perl 0.6.11 also accepted and ignored `--basename` in `--hardtrim5`, `--hardtrim3`, `--clock` and `--implicon` mode: those subs build the output name from the input file name and exit before the basename renaming in `trim()` / `validate_paired_end_files()`. It never honoured the flag in these modes, so no supported behaviour is removed; a command line that passed `--basename` to one of them (without effect) now fails instead. Perl had no uBAM input.

## Testing

- New unit test `cli::tests::test_validate_basename_rejected_with_specialty_modes` (all four modes).
- New integration test `integration_ubam::paired_interleaved_ubam_rejects_basename`: runs `--paired --basename foo` on `test_files/ubam_paired_test.bam` with both output formats and asserts a non-zero exit, the error text, and an empty output directory.
- Both fail without the fix (the integration test fails with `fastq: --basename must be rejected`).
- `cargo test`: all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output change. Only command lines that previously ran with `--basename` ignored are now rejected.

## Suggested CHANGELOG entry

- **`--basename` is refused where it would be ignored.** `--hardtrim5`, `--hardtrim3`, `--clock`,
  `--implicon` and single-file interleaved uBAM input (`--paired` with one BAM) always name their
  output after the input file, so `--basename` was silently dropped (as it was in Perl v0.6.x for
  the specialty modes). These combinations now fail before any output is written.

Part of #546 (finding 13 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7e7a19e1e37`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.