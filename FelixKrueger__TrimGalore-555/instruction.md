# Issue

**Title:** fix(demux): compress per-barcode outputs on one thread each

## Description

## Problem

`demultiplex` passed `--cores` to every per-barcode writer and to the NoCode writer. In `FastqWriter::create`, `cores > 1` with gzip means a `gzp` `ParCompress` with `cores` threads and its own buffers, per writer. Memory therefore grew with barcodes × cores.

Measured with `/usr/bin/time -l` on `test_files/demux_test.fastq.gz` (10K reads) and a 200-barcode sheet (the first 200 ACGT 4-mers), `--no_poly_g`:

| | `--cores 1` | `--cores 8` |
|---|---|---|
| before | 88.6 MB | 712.5 MB |
| after | 88.5 MB | 89.7 MB |

On the same input concatenated 50× (500K reads), 200 barcodes, `--cores 8`: 772.7 MB → 106.5 MB.

## Fix

Each demux writer is created with `1` thread (the single-threaded `flate2` `GzEncoder` path). The `cores` parameter of `demultiplex` is then unused and is removed (one caller in `main.rs`, one in the tests). Trimming itself still uses `--cores`; only the post-trim demux pass changes.

## Cost

The demux pass loses parallel compression. On the 500K-read input with the 3-barcode CI sheet at `--cores 8`, total wall time went from 0.49 s to 0.62 s (three runs each, stable). I also tried splitting the thread budget, `(cores / (barcodes + 1)).max(1)`: it ran in 0.65 s, so it recovers nothing and is not worth the extra line.

## Testing

- No new test: the change is to memory use, not output, and thread-pool count is not observable from a unit test without new hooks. The RSS numbers above are the evidence.
- Decompressed output of all 202 `.fq.gz` files from the 200-barcode `--cores 8` run is md5-identical before and after.
- `cargo test`: all suites pass (845 tests). `test_demultiplex_short_reads_route_to_nocode` and `tests/integration_output_collision.rs` cover the demux writer path.
- `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

Decompressed output is unchanged. The compressed bytes of demux files written with `--cores > 1` change (gzp vs flate2 stream framing; 6 of 202 files differed in compressed size by a few bytes up to 0.5%). The CI demux validation runs at the default `--cores 1` and compares `gzip -dc | md5sum`, so it is unaffected either way. At `--cores 1` the files are byte-identical to before.

## Suggested CHANGELOG entry

- **`--demux` memory no longer grows with barcodes × `--cores`.** Every per-barcode output had its
  own `--cores`-thread compression pool; a 200-barcode run peaked at 712 MB with `--cores 8`. The
  demux outputs are now compressed on one thread each (90 MB for the same run); decompressed output
  is unchanged.

Part of #546 (finding 7 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97154e778ea8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.