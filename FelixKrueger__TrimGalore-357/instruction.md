# Issue

**Title:** fix(ubam): run FastQC on --output-format ubam output

## Description

## Summary

The `run_ubam_output_*` driver functions in `src/main.rs` never called `fastqc::run`, so `--fastqc` was silently a no-op on `--output-format ubam`. The FASTQ-output path already honoured `--fastqc`. This PR wires the same guarded `fastqc::run` invocation into all three uBAM-output drivers (SE, PE two-file, PE interleaved) so the flag composes as any reader would expect.

`fastqc-rust` reads `.bam` natively (verified against the crate's `runner.rs` — `.bam`/`.ubam`/`.sam` extensions are dispatched to the BAM reader), so the report is produced directly from the trimmed BAM output. No intermediate conversion.

- SE uBAM output → one `*_trimmed_fastqc.zip` next to `*_trimmed.bam`
- PE uBAM output (single interleaved BAM) → one `*_val_fastqc.zip` next to `*_val.bam`, covering both mates. Unlike the FASTQ paired path which calls FastQC twice (once per output file), the uBAM paired path calls it once — regression-guarded by an explicit "exactly 1 zip" assertion.

## Context

Called out in the session handoff from the `--clump_only` v2 work (PR #356) as a pre-existing bug — v2's clump-only uBAM-output path correctly wires FastQC in, whereas the older trim uBAM output path did not. This closes the gap.

Independent of PRs #355 and #356 (which touch the same file); safe to merge in any order. Untouched by clump-only work — it's a defect in the trim uBAM output path that predates that feature.

## Test plan

- [x] `cargo fmt --all -- --check` — clean
- [x] `cargo clippy --all-targets --release -- -D warnings` — clean
- [x] `cargo test` — 355 tests, 0 failed
- [x] Local smoke: `--output-format ubam --fastqc test_files/ubam_test.bam` → produces `ubam_test_trimmed_fastqc.zip` + `.html`
- [x] Local smoke: `--paired --output-format ubam --fastqc test_files/ubam_paired_test.bam` → produces exactly one `ubam_paired_test_val_fastqc.zip`
- [ ] CI `validation-ubam` job: two new smoke steps (SE + PE with `--fastqc`) assert the zip is produced and PE emits exactly one

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edc8434f2d89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.