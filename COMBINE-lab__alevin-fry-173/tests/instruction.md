# Issue

**Title:** deps: trim unused Needletail compression and Polars test graph

## Description

## What

This PR narrows two dependency surfaces that alevin-fry does not need:

1. It disables `needletail`'s default compression feature. Every in-tree use is under `needletail::bitkmer`; alevin-fry does not use Needletail's FASTX parser.
2. It removes the test-only `polars` and `polars-io` dependencies. The two affected integration assertions now parse `featureDump.txt` with an explicit ten-column typed TSV schema using the already-present `csv` crate.

## Why

Needletail's compression feature brought in bzip2, xz, gzip, and zstd implementations for a parsing path that this crate never invokes. Disabling it removes `bzip2-sys`, `liblzma-sys`, and Needletail's zstd path without changing runtime code.

Polars was used only to validate two `featureDump.txt` files in integration tests. Its test graph was much larger than the functionality being exercised and brought in additional native build paths through `zstd-sys` and `stacker -> psm`. The replacement parser preserves the relevant regression guarantees:

- the header is exactly the expected ten columns;
- every data row has exactly ten fields;
- barcode and sample-name fields are non-empty strings;
- count and rate columns parse as their expected numeric types;
- the observed sample names match the expected wells.

Relative to the original PR head, the normal/build/dev dependency tree falls from 594 to 331 lines and `Cargo.lock` loses 1,435 net lines.

## Scope

This is intentionally **not** a claim that alevin-fry is C-toolchain-free. Two production native dependencies remain unchanged by design:

- `libdeflater -> libdeflate-sys`, used for compressed ATAC temporary BED buckets;
- `mimalloc -> libmimalloc-sys`, used as alevin-fry's required global allocator.

After this PR, those are the only paths from alevin-fry's normal test graph to Cargo's `cc` crate. The value of this change is removing unused and disproportionate dependency surface, not eliminating all native code.

## Validation

- formatting and diff checks pass;
- `cargo clippy --workspace --all-targets --all-features -- -D warnings` passes;
- `cargo test --workspace`: 24 passed, 1 intentionally ignored, 0 failed;
- isolated `cargo build --release` passes;
- the existing end-to-end output comparison found zero differing cells across 26,126 cells.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c82c0ba8432`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.