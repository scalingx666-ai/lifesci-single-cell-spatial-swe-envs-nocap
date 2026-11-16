# Issue

**Title:** refactor(trimmer): share the per-read trim, stats and filter step across all paths

## Description

## Problem

The per-read body (count the read, `trim_read`, add quality / adapter / RRBS / poly-A / poly-G stats, `--discard_untrimmed`, `total_bp_after_trim`, then the length / max-length / max-N filter and its counters) was written out six times:

- `src/trimmer.rs`: `run_single_end`, `run_paired_end`, `run_single_end_to_bam`, `run_paired_end_to_bam`
- `src/parallel.rs`: `classify_single`, `classify_paired`

#541 (`bp_after_cutadapt` on the parallel path) and #544 (where `r1_unpaired` / `r2_unpaired` are counted) were both cases of a fix reaching some copies and missing others.

## Fix

Pure move plus call sites, no behaviour change:

- `classify_single`, `classify_paired`, `SingleOutcome` and `PairOutcome` move unchanged from `parallel.rs` into `trimmer.rs`, as `pub(crate)`. `parallel.rs` imports them from there.
- The four serial loops call them and keep only their own I/O:
  - `run_single_end` / `run_single_end_to_bam`: write the record on `Pass`.
  - `run_paired_end`: writes R1/R2 and the passthrough record (`passthrough_records_kept`) on `Pass`; counts `passthrough_records_dropped` on `Discarded` and `Unpaired`; on `Unpaired` writes the rescue records and counts `r1_unpaired` / `r2_unpaired` at the write site, as #544 left it. The three-way read-ID sync check and `passthrough_records_checked` stay in the loop.
  - `run_paired_end_to_bam`: writes the interleaved pair on `Pass` and ignores `Unpaired`, as it ignored `TooShort` before (`--retain_unpaired` is rejected for uBAM output).

Net: `src/trimmer.rs` and `src/parallel.rs`, 219 insertions, 466 deletions (−247 lines).

## Testing

The existing tests guard the moved code; none were changed:

- `parallel::tests::test_parallel_serial_trim_stats_parity`, `test_parallel_serial_bp_after_trim_parity_with_clipping`, `test_parallel_serial_bp_after_trim_parity_paired`, `test_parallel_serial_unpaired_counter_parity`, `test_clumpy_stats_parity_with_plain`, `test_passthrough_serial_smoke`, `test_passthrough_serial_parallel_parity`
- `tests/integration_passthrough.rs`, `tests/integration_ubam_out.rs`, `tests/integration_poly.rs`, `tests/integration_library.rs`, plus the `trimmer::tests` unit tests

`cargo fmt --all -- --check`, `cargo clippy --all-targets --release -- -D warnings` and the full `cargo test` suite (845 tests) pass.

As an extra check, I built `origin/dev` and this branch and compared outputs on the bundled fixtures for: SE; PE with `--retain_unpaired --length 60`; PE `--rrbs --poly_a`; PE `--passthrough`; SE uBAM out with `--discard_untrimmed`; PE uBAM out with `--length 60 --max_n 2`; and PE `--cores 4 --retain_unpaired`. The decompressed FASTQ outputs and the trimming reports were identical. The uBAM records (`samtools view`) and the non-`@PG` header were identical; the only difference was the `@PG CL:` binary path.

## Byte-identity

No output byte changes on any path, including the Perl-validated SE and PE paths.

## Suggested CHANGELOG entry

- **One shared per-read trim and filter step for every trimming path.** The serial FASTQ, serial
  uBAM and `--cores N` paths now all call the same `classify_single` / `classify_paired` in
  `trimmer.rs` instead of six hand-kept copies, so a stats fix can no longer reach only some of
  them (as happened with #541 and #544). No change in output.

Part of #546 (finding 15 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a7b64d9deb2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.