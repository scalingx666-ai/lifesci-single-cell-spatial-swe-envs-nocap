# Issue

**Title:** fix(bam): accept SEQ=* records and UInt32 tags on the uBAM paths

## Description

## Problem

Two kinds of valid uBAM input aborted the run:

1. **Empty sequence.** `bam_record_to_fastq` bailed with `BAM record has empty sequence` on a record with `SEQ = *`. The same read as FASTQ (`@r` / empty line / `+` / empty line) is accepted and simply filtered by `--length` like any short read.
2. **Integer tags above `i32::MAX`.** The read side renders every BAM integer width (`Int8`, `UInt8`, `Int16`, `UInt16`, `Int32`, `UInt32`) as `i:<value>` in the FASTQ header, but the uBAM writer parsed `i:` with `parse::<i32>()`. A record carrying `XN:i:3000000000` (stored as `UInt32`) therefore failed under `--preserve-tags XN --output-format ubam` with `invalid i: tag value "3000000000"`.

## Fix

1. Remove the empty-sequence bail. An empty `QUAL` (or the `0xFF` missing-quality sentinel) already maps to an empty quality string, so the record becomes an empty FASTQ read and goes through the same trimming and length filtering as one read from FASTQ.
2. Parse `i:` as `i64` and store `Int32` when the value fits, `UInt32` when it fits there, and fail with `i: tag value N is outside the BAM integer range (-2147483648..=4294967295)` otherwise. That range is the union of all widths the read side can produce, so every integer tag read from a BAM now round-trips.

## Testing

- `bam::tests::i_tag_above_i32_max_round_trips_and_out_of_range_rejected`: writes `@read1\tXN:i:3000000000\tXM:i:-2147483648` with `BamWriter`, reads it back with `XN,XM` preserved and checks the id is identical; also checks `4294967296` and `-2147483649` are rejected with the new message.
- `bam::tests::empty_sequence_record_reads_as_empty_fastq_read`: writes an empty-sequence record followed by a normal one and checks the reader yields `("@empty", "", "")` and then the next record.
- Both tests fail with the old code (the old i32-only parse and the empty-sequence bail restored temporarily).
- Manual end-to-end check with a `samtools view -b` input holding one normal read (`XN:i:3000000000`) and one `SEQ=* QUAL=*` read: `--preserve-tags XN --output-format ubam --length 0` writes both records with the tag intact; FASTQ output drops the empty read as too short, as for FASTQ input.
- `cargo test` (whole suite, `--no-fail-fast`): all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

No existing test asserted the old behaviour.

## Byte-identity

Only uBAM input/output code changes. Inputs that worked before produce the same bytes; `i:` values within the `i32` range are still stored as `Int32`. The Perl-validated FASTQ paths (SE, PE, hardtrim5, clock, demux) are not touched.

## Suggested CHANGELOG entry

- **uBAM records with `SEQ = *` and integer tags above 2147483647 no longer abort the run.** An empty-sequence record now becomes an empty read, as it would from FASTQ, instead of failing with `BAM record has empty sequence`. Under `--preserve-tags … --output-format ubam`, an unsigned 32-bit tag such as `XN:i:3000000000` is now written back as `UInt32` instead of failing to parse as a signed 32-bit integer.

Part of #546 (finding 11 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da92ec89645d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.