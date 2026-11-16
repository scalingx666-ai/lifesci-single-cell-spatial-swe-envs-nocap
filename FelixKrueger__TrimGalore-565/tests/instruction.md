# Issue

**Title:** fix(reader): treat a closed reader channel without the EOF marker as an error

## Description

## Problem

`FastqReader::next_record` (threaded mode, `src/fastq.rs`) and `BamReader::next_record` (threaded mode, `src/bam.rs`, shared by the single-file and the paired de-interleaved readers) both had:

```rust
Err(_) => Ok(None), // channel closed
```

So if the background reader thread panicked part-way through a file, its sender was dropped, the consumer saw a normal end of file, and the run published a truncated output with exit 0. #434 fixed the same pattern for the worker threads.

## Producer paths checked

Every exit of every producer sends the empty-batch EOF marker or an `Err` before dropping its sender:

- FASTQ threaded reader: open failure → `Err`; EOF → remaining batch, then the empty marker; parse error → `Err`.
- BAM single threaded reader: open failure → `Err`; EOF → remaining batch, then the empty marker; conversion or read error → `Err`.
- BAM paired de-interleaver: open failure, invalid flag bits, conversion error, read error, orphans at EOF, and `MAX_SLACK` overflow all send `Err` on both sides; clean EOF sends the empty marker on both sides.

The only other exit is a `send` failing because the receiver was dropped. For the single readers nobody is left to read. For the paired reader, the R1 and R2 readers are always created, consumed in lockstep, and dropped together (`main.rs`, `clump_only.rs`, `parallel.rs`), so one side never keeps reading after the other is gone.

## Fix

Both `Err(_)` arms now `bail!` with "... reader thread ended without signalling end of input".

## Testing

- `fastq::tests::threaded_reader_closed_without_eof_marker_is_an_error`: sends one batch, drops the sender without the marker; the first record still arrives, the next call returns `Err`.
- `bam::tests::threaded_reader_closed_without_eof_marker_is_an_error`: same contract for `BamReader`.

Both fail with the old `Ok(None)` arms and pass with the fix.

`cargo test`: all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output change. Only a reader-thread crash, which used to give truncated output, now gives an error.

## Suggested CHANGELOG entry

- **A crashed input-reader thread now fails the run instead of truncating the output.** The threaded FASTQ and uBAM readers treated a closed channel as end of file, so a reader thread that panicked mid-file left a short output with exit 0; since every normal exit sends an explicit end marker first, a closed channel without it is now an error, as #434 already did for the worker threads.

Part of #546 (finding 10 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52d279be65b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.