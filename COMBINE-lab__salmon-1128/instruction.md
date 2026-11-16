# Issue

**Title:** test(map): bench the alignment kernel with divan instead of a hand-rolled loop

## Description

`examples/bench_align` timed the alignment kernel by running a fixed iteration count and dividing wall clock by the number of alignments. That reports one number per run with no distribution behind it, and the number moved by up to 28% between runs of the same binary on the same input, wider than every change the mapper has been getting. The harness could not separate a real regression from scheduler noise.

The same workload is now `crates/salmon-map/benches/align.rs` under divan, which runs each case to a time budget and reports fastest / median / mean / sample count.

### Measured stability

Three consecutive runs of the anchored path, median per case (256 alignments per sample):

| case | run 1 | run 2 | run 3 | spread |
|---|---|---|---|---|
| 51 bp, 0 mm | 5.624 µs | 5.499 µs | 5.666 µs | 3.0% |
| 100 bp, 0 mm | 9.082 µs | 9.895 µs | 9.624 µs | 8.9% |
| 150 bp, 0 mm | 11.52 µs | 11.33 µs | 11.54 µs | 1.9% |
| 51 bp, 2 mm | 5.957 µs | 5.812 µs | 5.958 µs | 2.5% |
| 100 bp, 2 mm | 10.10 µs | 10.24 µs | 10.54 µs | 4.4% |
| 150 bp, 2 mm | 11.95 µs | 11.79 µs | 12.12 µs | 2.8% |

The old loop, same machine, same case (51 bp / 0 mm): 21.7, 24.8, 27.8 ns per alignment across three runs.

### Also

- Cases are selectable: `cargo bench -p salmon-map -- anchored`, or by read length, instead of the binary always running all twelve.
- An `ItemsCount` counter reports alignments per second directly.
- The sequence generator and both `AlignConfig` paths are unchanged, so this measures the same workload the example did.

`divan` is a dev-dependency only. The workspace already has `criterion` for `salmon-infer`'s `em_step`; this does not touch it, though the two could be consolidated later if you would rather have one harness.

`cargo test --workspace`, `cargo clippy --workspace --all-targets`, `cargo fmt --check` all clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d19bb9cdeb4f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.