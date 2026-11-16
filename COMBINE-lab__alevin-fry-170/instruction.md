# Issue

**Title:** perf(build): abort on panic in the release profile

## Description

## What

Sets `panic = "abort"` in `[profile.release]`, and records next to the commented-out `codegen-units = 1` why that one was measured and rejected.

## Measurements

Toy dataset from the `sample_run` CI job (29.5M reads, 26,126 cells, 375,446 refs, 78,899 genes). Apple M-series, 16 cores, 128 GB, macOS 26.6, `rustc 1.97.1`, `-t 8`.

Timings come from an **interleaved** A/B: all variants alternate within each repetition rather than one variant being run to completion and then the next. Blocked runs on this host drift by more than the effect being measured (the same binary measured 1.71s and 3.11s for `generate-permit-list` in two consecutive sessions); interleaving puts that drift on every variant equally. Median of 9 repetitions, range in brackets.

| phase | base | `panic="abort"` | `abort` + `codegen-units=1` |
|---|---|---|---|
| `generate-permit-list` | 1.523 [1.50-1.85] | 1.533 [1.50-2.44] (+0.7%) | 1.526 [1.50-1.76] (+0.2%) |
| `collate` | 1.825 [1.78-2.09] | 1.844 [1.82-2.21] (+1.0%) | 1.899 [1.88-1.96] (+4.1%) |
| `quant -r cr-like` | 0.912 [0.91-1.00] | 0.905 [0.90-1.07] (-0.8%) | 0.871 [0.86-0.94] (-4.5%) |
| `quant -r cr-like-em --small-thresh 0` | 5.712 [5.67-8.16] | **4.597 [4.57-5.51] (-19.5%)** | 4.576 [4.56-4.81] (-19.9%) |

Build and size, crate-only rebuild (`touch src/*.rs src/atac/*.rs`, dependencies warm):

| variant | rebuild | binary |
|---|---|---|
| base | 6.64 s | 5,562,544 B |
| `codegen-units=1` | 20.07 s | 4,772,576 B (-14%) |
| `panic="abort"` | 5.70 s | 4,499,472 B (-19%) |
| both | 23.03 s | 3,959,664 B (-29%) |

`codegen-units = 1` is rejected on those numbers: stacked on `panic = "abort"` it is worth another 0.4% on the EM path, costs 4% on `collate`, and triples the crate rebuild. It stays commented out with the measurement written next to it so the question does not have to be reopened from scratch.

The EM path is where the win lands because that is the only compute-bound stage; `collate` is I/O bound and `generate-permit-list` is dominated by reading the 1.2 GB RAD file.

## Output equivalence

`generate-permit-list` + `collate` + `quant` run with each variant, then every nonzero of `quants_mat.mtx` re-keyed by its barcode and compared: **0 of 26,126 cells differ**, for both `cr-like` and `cr-like-em`.

The comparison is done that way rather than on raw bytes because the pipeline is already not byte-reproducible run to run, even from a single unmodified binary: three consecutive baseline runs produced three different `quants_mat.mtx`, `quants_mat_rows.txt`, `permit_map.bin`, `permit_freq.bin` and `map.collated.rad`, while the per-barcode count vectors were byte-identical. The cells are emitted in a different order; the counts do not change. That is pre-existing and unrelated to this PR, but it is the reason "the bytes changed" cannot be the acceptance criterion here.

## Behaviour change

`panic = "abort"` is not purely a build flag, so, explicitly:

- No `catch_unwind` anywhere in the crate, and the only interaction with mutex poisoning is `unwrap`, so nothing depended on unwinding.
- A panicking worker thread now aborts the process instead of surfacing later as a `join` error. For a batch CLI that is the better outcome (no partial output written after a thread has already failed), but it is a real difference in what a user sees.
- Cargo ignores `panic` for the test and bench profiles, so the `#[should_panic]` test in `src/utils.rs` still runs unwound. CI runs `cargo test` in the dev profile and is unaffected.
- `[profile.dist]` inherits from `release`, so cargo-dist release binaries pick this up too. That is intended.

## Checks

- `cargo test --workspace`: 24 passed, 1 ignored, 0 failed
- `cargo clippy --workspace --all-targets`: clean
- `cargo build --release`: no warnings

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c82c0ba8432`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.