# Issue

**Title:** refactor(filters): bundle unpaired-rescue thresholds into UnpairedLengths struct

## Description

## Summary
- Pure parameter-shape refactor — no behaviour change, no new flags, no new tests needed.
- Bundles the per-side minimum-length thresholds for `--retain_unpaired` into one struct `UnpairedLengths { r1, r2 }`. These two values are set together at CLI parse and threaded unchanged through `filter_paired_end`, `run_paired_end`, and the parallel pipeline, so they belong together.
- Retires one `#[allow(clippy::too_many_arguments)]` on `process_paired_batch` (8 → 7 args — exactly at clippy's default threshold). The other two hot-path entrypoints (`run_paired_end_parallel`, `process_pairs`) stay at 10 args and keep the attribute — a broader config-bundle refactor for those is tracked separately.

## Why now
Came out of a brief survey of the three `#[allow(clippy::too_many_arguments)]` sites. This is the narrow, obviously-correct slice — two fields that always travel together and have the same semantic role (per-side unpaired-rescue minimums). The other two sites would need a larger design conversation about config grouping, so they stay as-is for this beta.

## Test plan
- [x] `cargo build --release` clean
- [x] `cargo test --release` — 99 passed, 0 failed (the 2 paired-filter tests use the new struct literal)
- [x] `cargo clippy --all-targets --release -- -D warnings` silent (confirms the removed `#[allow]` on `process_paired_batch` is fine at 7 args)
- [x] `cargo fmt --all -- --check` silent
- [ ] CI green on PR

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9afbada85dc5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.