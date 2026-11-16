# Issue

**Title:** chore: remove dead report and clump_only code

## Description

## What

Deletes code that nothing calls or that can never run:

- `report::write_run_stats` (about 100 lines). No caller in `src/`, `tests/` or `examples/`. The text report is written by `write_report_header`, `write_cutadapt_compatible_section`, `write_run_footer` and `write_pair_validation_stats`.
- `clump_only::expected_output_paths_single` and `clump_only::expected_output_paths_paired`. No caller; they only forwarded to `naming::clumped_output_name` / `naming::clumped_paired_output_names`, which the pre-flight already calls directly and which stay.
- In `clump_only_paired_to_bam_one_pair` (two-file Shape A), the `let header = if matches!(fmt, InputFormat::UnalignedBam) { Some(peek_header(..)) } else { None }` branch. The `bail!` right above it rejects any uBAM in either file, so `header` was always `None`. `source_header` is now set to `None` directly.

Net: 2 files changed, 1 insertion, 129 deletions (`git diff --stat origin/dev`).

## Behaviour

No behaviour change. The functions had no callers (checked with grep over `src/`, `tests/`, `examples/`), and the removed branch was unreachable. Shape A clump-only uBAM output is covered by `tests/integration_clump_only_ubam.rs` (`pe_ubam_out_interleaved_from_fastq_pair`, `multi_pair_pe_bam_produces_one_output_per_pair`, `rejects_two_bam_paired`, `rejects_mixed_format_paired`).

## Testing

- `cargo test`: 845 passed, 0 failed.
- `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output changes on any path.

## Suggested CHANGELOG entry

None needed (internal cleanup). If one is wanted:

- **Removed unused internal code.** `report::write_run_stats`, `clump_only::expected_output_paths_single` / `_paired` and an unreachable branch in the clump-only paired uBAM path had no callers. No change in behaviour.

Part of #546 (finding 16 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c98c98b56b96`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.