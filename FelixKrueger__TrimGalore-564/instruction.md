# Issue

**Title:** fix(fastq): reject records that are not one 4-line FASTQ record

## Description

## Problem

`FastqReader` takes four lines per record and checked nothing about them; only `sanity_check` looked at the first record's `@`. So:

- A wrapped (multi-line) FASTQ such as `@r1 / ACGT / ACGT / + / IIII / IIII` is cut into garbage records (the second "record" has id `ACGT`), written out, exit 0.
- A 40 bp read with 30 quality characters is written out as invalid FASTQ, exit 0.
- A non-ASCII byte in a sequence (`AéT`, 4 bytes) panics `--clip_R1`, `--hardtrim5` and `--clock` with "byte index is not a char boundary".

Cutadapt, which Perl Trim Galore 0.6.x used, rejects all three.

The Direct arm of `FastqReader::next_record` was also a line-for-line copy of `read_next_direct`, which the threaded reader uses, so any fix had to be made twice.

## Fix

- The Direct arm now calls `read_next_direct`; there is one parser for the sync and threaded readers. Its signature changes from a `&mut (Box<dyn BufRead>, String)` tuple to `(reader, line_buf)` so both callers can pass their state.
- The parser bails unless the header starts with `@`, the third line starts with `+`, `seq.len() == qual.len()`, and sequence and quality are ASCII. Each message names the record id (or quotes the offending header line).
- The first-record `@` check in `sanity_check_with` is now unreachable and is removed. Errors from that first read get the file name as context (`Failed to read the first record of input file '...'`), so the file is still named. The empty-file and colorspace checks are unchanged.

## Testing

New unit tests in `src/fastq.rs`: `wrapped_fastq_is_rejected`, `header_without_at_is_rejected`, `seq_qual_length_mismatch_is_rejected`, `non_ascii_sequence_is_rejected`, `threaded_reader_rejects_malformed_record`. All five fail with the four checks disabled and pass with them.

Negative fixtures checked by hand: `colorspace_file.fastq` still gives the SOLiD colorspace error, `empty_file.fastq` the empty-file error, `truncated.fq.gz` the deflate error. Every FASTQ fixture in `test_files/` passes the new checks.

`cargo test`: all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No change to output for valid input: the checks only add errors on records that are not valid 4-line FASTQ.

## Suggested CHANGELOG entry

- **Malformed FASTQ records are now rejected instead of passed through.** A wrapped (multi-line) FASTQ, a record whose sequence and quality differ in length, or a record with non-ASCII bytes was accepted with exit 0 (or, for non-ASCII under `--clip_R1` / `--hardtrim5` / `--clock`, crashed); every record is now checked for `@`, `+`, equal lengths and ASCII, as Cutadapt does, and the error names the record.

Part of #546 (finding 2 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58d669b08d34`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.