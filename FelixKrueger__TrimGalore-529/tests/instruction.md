# Issue

**Title:** feat(ubam): multithreaded uBAM input and output with --cores

## Description

## Multithreaded uBAM output and input (`--cores`)

`--output-format ubam` was single-threaded and ignored `--cores`, and uBAM input was read and converted on one thread. Records, record order, header and statistics are the same at every core count.

### What changes

- **uBAM output uses `--cores`.** Workers trim and encode batches, a BGZF pool compresses them, and the batches are written in input order. `--cores 1` keeps the serial path. README, `CLAUDE.md` and the help text are updated.
- **uBAM input is converted on a worker pool** when `--cores > 1`.
- **`--preserve-tags` are read in one pass per record**.

### Performance

5M reads (single-end) or 5M pairs (paired-end), uBAM in and out, from a 150 bp paired-end single-cell library, one run each. The run used adapter trimming (`--stringency 3`), `--poly_g` and `--preserve-tags` with 15 tags.

Both builds are glibc, compiled the same way: v2.3.0 is `c6528e5` (it ignores `--cores` for uBAM output), and the other is this branch. Measured in a single 16-CPU Slurm job. The input was read from network storage (cached after the first read) and the output went to local disk. Speed-up is against v2.3.0.

| Input | Build | `--cores` | Time (s) | Speed-up | Peak RSS (MB) |
|---|---|---|---|---|---|
| single-end | v2.3.0 | any | 92.3 | 1.0× | 5 |
| single-end | this branch | 1 | 85.6 | 1.1× | 6 |
| single-end | this branch | 2 | 27.8 | 3.3× | 72 |
| single-end | this branch | 4 | 23.2 | 4.0× | 84 |
| single-end | this branch | 8 | 16.3 | 5.7× | 139 |
| single-end | this branch | 16 | 18.5 | 5.0× | 246 |
| paired-end | v2.3.0 | any | 142.1 | 1.0× | 34 |
| paired-end | this branch | 1 | 140.4 | 1.0× | 35 |
| paired-end | this branch | 2 | 45.6 | 3.1× | 170 |
| paired-end | this branch | 4 | 27.5 | 5.2× | 334 |
| paired-end | this branch | 8 | 19.7 | 7.2× | 627 |
| paired-end | this branch | 16 | 24.6 | 5.8× | 843 |

The records and the header (except the `@PG` line) are identical in all runs, including v2.3.0: the MD5 of the header without `@PG` plus the records is the same for every run of an input. There is no further gain beyond 8 cores on this node, whose 16 CPUs are 8 physical cores. Memory grows with `--cores` because more batches are in flight.

### Testing

- New tests compare the serial and the parallel paths over several batches: the decompressed BAM stream, header and all statistics (paired and single-end output), and the records, their order and the errors of the pooled and plain uBAM readers.
- `cargo fmt --all -- --check` and `cargo test --release` pass (357 tests).

### Notes

- No new dependencies.
- `cargo clippy -- -D warnings` with Rust 1.99 flags 5 `byte_char_slices` lints in test code that are already on `dev`.

With the help of Claude Code.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d324437ac033`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.