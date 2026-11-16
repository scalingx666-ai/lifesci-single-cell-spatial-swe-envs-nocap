# Issue

**Title:** feat(quant): add chunked BAM mapping output

## Description

## Summary

This adds `salmon quant --writeBam <FILE>`, which writes the retained mapping
records as unsorted, BGZF-compressed BAM. The records are semantically equivalent
to `--writeMappings` SAM output, including paired, orphan, and single-end flags;
spoofed overhang-aware CIGARs; sequence orientation; mate coordinates; template
length; mapping quality; and `NH`/`HI`/`XT`/`AS` tags.

This feature was proposed and initially implemented by @BenjaminDEMAILLE in
#1029. Thank you, Benjamin, for identifying a useful downstream need, choosing
BAM rather than reference-dependent CRAM, and providing the original working
implementation and round-trip test. This PR is a fresh implementation based on
current `develop`, building on that proposal.

## Why a fresh implementation?

#1029 established the feature and its desired behavior. While reviewing it, we
saw an opportunity to integrate BAM output more deeply with the existing SAM
path and to optimize for large mapping outputs. The principal implementation
differences are:

- SAM and BAM now share one format-neutral, borrowed alignment-record builder
  instead of maintaining two copies of flag, coordinate, CIGAR, sequence, and
  tag logic.
- Mapping workers encode BAM records independently into reusable raw-BAM chunks,
  rather than buffering owned `RecordBuf` objects and serializing/compressing
  them while holding a global writer mutex.
- A bounded channel carries whole chunks (normally many records and up to a
  2 MiB target), not individual alignments. Sending a chunk moves only the
  `Vec` descriptor; it does not copy its backing allocation.
- A dedicated ordering thread feeds the raw record stream into noodles'
  multithreaded BGZF writer. Record encoding and BGZF compression can therefore
  proceed in parallel, while the small portion that inherently must be ordered
  remains centralized.
- Empty chunk buffers are recycled back to mapping workers. Initial buffers are
  modest (64 KiB), grow only as needed, retain useful capacity, and discard
  unusually large allocations above a retention ceiling.
- Output errors from SAM/BAM encoding, channels, compression, file writes, or
  finalization propagate back through quantification rather than being ignored.

These changes add some pipeline machinery, but kindly aim to preserve the spirit
of #1029 while improving long-run maintainability, bounding memory, reducing
allocation, and avoiding compression or record serialization inside a global
critical section.

## Design

### Shared record semantics

`mapping_record.rs` emits short-lived `AlignmentRecord<'_>` views. Names and
sequences are borrowed from the input reads, CIGAR storage is an inline
two-operation array (the spoofed CIGAR needs at most a match plus soft clip), and
the four auxiliary tags are plain fields. No owned record graph is created.

Both output formats consume these views immediately:

- SAM formats directly into its reusable per-worker `String`.
- BAM writes the binary record representation directly into its reusable
  per-worker `Vec<u8>`.

This gives the record semantics one source of truth and prevents SAM/BAM drift.
Reverse-complemented sequence is emitted directly in reverse order, without a
temporary sequence allocation.

### Chunked BAM pipeline

Each mapping worker accumulates complete uncompressed BAM records in a private
chunk. Chunks are handed off at the size threshold and at existing batch/thread
boundaries. The bounded queue provides backpressure, so memory does not grow
with input size.

The writer thread preserves chunk order and submits bytes to
`noodles_bgzf::io::MultithreadedWriter`, which distributes BGZF block compression
while preserving file order and writes the required EOF block. Successfully
written chunks are cleared and returned through a bounded recycle queue.

The BAM header includes `@HD`, every index reference (including decoys), and a
`@PG` record with Salmon version and command information.

### Interface

`--writeMappings` and `--writeBam` are intentionally mutually exclusive. Clap
rejects the combination for CLI callers, and `salmon_quant::quantify` repeats
the validation for library callers.

Record order is unspecified because mapping is parallel. The documentation
advises sorting when a downstream consumer requires coordinate or query-name
order.

## Correctness

The end-to-end parity test quantifies the same input twice with four mapping
threads, once to SAM and once to BAM. Both files are parsed through noodles into
the same semantic record type, normalized for unspecified worker completion
order, and compared as complete record multisets. This checks flags, coordinates,
MAPQ, CIGAR, mate fields, template length, sequence orientation, qualities, and
all tags—not merely that the BAM can be opened.

Additional coverage verifies library-level mutual exclusion and the presence of
the BAM program header.

## Verification

- `cargo test --workspace --release`
- `cargo clippy -p salmon-quant -p salmon-cli --all-targets --no-deps -- -D warnings`
- `cargo fmt --all -- --check`
- `git diff --check`
- direct CLI check that `--writeMappings` and `--writeBam` conflict

Closes the feature request embodied by #1029; #1029 can be superseded by this
implementation while retaining full credit for the original contribution.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a0755e35934`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.