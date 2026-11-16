# Issue

**Title:** perf(alloc): use mimalloc as the global allocator

## Description

## What

Sets `mimalloc` as the binary's `#[global_allocator]`. Two-line change plus the dependency, exact-pinned at `=0.1.52`.

## Why

The trimming hot loop allocates and frees small, short-lived buffers per record, across `--cores` workers that each own their chunk. mimalloc's sharded free lists have a shorter fast path than the platform malloc for that shape.

The size of the win depends on the path and the platform, so these are scoped rather than headlined. Measured on **4M simulated read pairs** (distinct inserts, 3'-degrading quality, 35% adapter read-through, so the gzip writer does real work), macOS/arm64, 3 runs, mean:

| path | cores | wall (stock → mimalloc) | peak RSS |
|---|---|---|---|
| plain trimming | 1 | 32.9 s → 31.1 s (-5%) | unchanged |
| plain trimming | 4 | 8.6 s → 7.8 s (-9%) | 104 → 103 MB |
| plain trimming | 8 | 4.7 s → 4.4 s (-7%) | unchanged |
| plain trimming | 16 | 3.7 s → 3.2 s (-12%) | unchanged |
| `--clumpify` | 4 | 9.8 s → 8.7 s (-11%) | 1284 → 979 MB (**-24%**) |

The RSS drop is specific to the memory-budgeted `--clumpify` path; plain trimming never holds enough live at once for it to show.

@FelixKrueger's independent replication at 6.8M pairs (macOS/arm64 + 128-core Linux) agrees on direction and lands the same on macOS plain trimming (8% vs my 9%), while showing `--clumpify` at ~18% on both platforms and Linux plain trimming at only 1.5%. That is the writer-bound picture from their profiling, and a compression-heavy dataset drops the Linux `--clumpify` gain to 4-6%. **So: this helps where the run is allocation-heavy rather than deflate-heavy, and least on Linux plain trimming.**

An earlier revision of this PR claimed a flat 25% at `--cores 8`. That number came from a fixture built by concatenating one 10K-read file 40 times, which compresses far too well and keeps the working set unrealistically small. It has been replaced by the table above.

## Why not snmalloc

`snmalloc-rs` 0.7.5 was built and benchmarked head-to-head, since its message-batched cross-thread free targets this producer/consumer shape. It lands **within noise** of mimalloc (CPU 2.38 s / 2.45 s / 2.38 s at 1/4/8 cores on the earlier fixture). Workers allocate and free mostly within their own chunk, and only the finished compressed buffer crosses threads, so the pattern snmalloc optimises for does not dominate here.

Tiebreak is therefore build cost: snmalloc needs a C++17 toolchain plus cmake, mimalloc is pure C and one dependency. `snmalloc-rs` also resolves to 0.3.8 by default under this crate's `rust-version = 1.88` floor.

## Invariants checked

- **Byte-identity**: `_val_1.fq.gz` / `_val_2.fq.gz` are byte-identical (`cmp`) to the pre-change binary on the 4M-pair input, so the `validation` job's md5 comparison against Perl 0.6.11 is unaffected.
- **Reproducible builds**: two `cargo clean` + `cargo build --release` runs under a fixed `SOURCE_DATE_EPOCH` produce the same SHA-256.
- **No external runtime deps**: links statically. Also builds clean for `aarch64-unknown-linux-musl` (+246 KB), though per @FelixKrueger no shipped target or container is musl and the bioconda recipe already declares `{{ compiler('c') }}`, so this costs nothing on shipped channels.
- `cargo test --release`: 729 passed, 0 failed. `cargo fmt --all -- --check` and `cargo clippy --all-targets --release -- -D warnings`: clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ffe86f5842a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.