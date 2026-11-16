# Issue

**Title:** fix(bam): reject paired uBAM mates whose read names differ

## Description

## Problem

For `--paired` with one interleaved uBAM, the background de-interleaver in `src/bam.rs` routes records into an R1 queue and an R2 queue by flag bit and pops one from each as soon as both are non-empty. It never compared the two read names. A file with an orphan R1 of read `B` followed by an orphan R2 of read `C` produced `@B` in `_val_1` lined up with `@C` in `_val_2`, and the run exited 0. Every later pair stays correct only if the orphans happen to cancel out; otherwise the two outputs are silently scrambled.

## Fix

When a pair is popped, compare the QNAMEs and fail if they differ. The FASTQ id built by `bam_record_to_fastq` is `@QNAME` plus an optional `\t`-joined `--preserve-tags` tail, and QNAMEs with whitespace are already rejected, so the name is the id up to the first tab. The error names the file, the BAM record index, both names and the same `samtools collate` remediation the existing `MAX_SLACK` error gives. No new options.

## Testing

- New unit test `bam::tests::paired_interleaved_rejects_mismatched_mate_names`: writes a BAM with pair `A` (R1 and R2 carrying different `XN` tag values, which must not count as a mismatch) followed by orphan R1 `B` and orphan R2 `C`; reads it with `--preserve-tags XN`-equivalent settings and asserts the error `mate names differ at BAM record 4 (R1 'B', R2 'C')` plus the `samtools collate` hint.
- With the check disabled the test fails (the mismatched records are paired without error).
- `cargo test` (whole suite, `--no-fail-fast`): all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

Only the uBAM input path changes. Correctly interleaved input produces the same output as before. The Perl-validated FASTQ paths (SE, PE, hardtrim5, clock, demux) are not touched.

## Suggested CHANGELOG entry

- **Paired uBAM input now fails when a mate's read name does not match.** The interleaved-uBAM de-interleaver paired R1 and R2 records in arrival order without comparing names, so an orphan R1 and an unrelated orphan R2 were written as one pair and `_val_1` / `_val_2` went out of sync with exit status 0. It now stops with the record number, both names and a `samtools collate` hint.

Part of #546 (finding 3 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52d279be65b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.