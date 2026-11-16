# Issue

**Title:** perf(cli): use available parallelism with a two-thread floor

## Description

## What

Replace alevin-fry's direct use of `num_cpus::get()` with
`std::thread::available_parallelism()`. The standard-library query accounts for
CPU affinity and cgroup quotas and avoids a direct dependency used only to
choose CLI defaults.

The maintainer follow-up also establishes a two-thread floor for every RNA and
ATAC command:

- an explicit request below 2 is accepted, logged as a warning, and raised to 2;
- requests of 2 or more are passed through unchanged;
- if `available_parallelism()` reports 1, a warning is logged and the default is
  raised to 2;
- if available parallelism cannot be determined, a warning is logged and the
  default is 2.

The `--threads` help for every affected command documents this behavior.

## Container behavior

The original contribution measured both queries in the same container on a
16-core host:

| container settings | `num_cpus::get()` | `available_parallelism()` |
|---|---:|---:|
| none | 16 | 16 |
| `--cpus=2` | 2 | 2 |
| `--cpuset-cpus=0,1` | 2 | 2 |
| `--cpus=1.5` | 2 | 1 |
| `--cpus=3.5` | 4 | 3 |

The two-thread floor intentionally overrides the reported value only when the
standard-library query returns 1. Values of 2 or greater remain unchanged.

## Dependency effect

This removes alevin-fry's **direct** `num_cpus` dependency. The crate remains in
the resolved normal dependency graph through `num_cpus <- sprs <- alevin-fry`.

## Checks

- `cargo fmt --check`
- `cargo clippy --all-targets --all-features -- -D warnings`
- `cargo test --all-targets --all-features` (37 passed, 1 ignored)
- `cargo build --release`
- CLI smoke tests for explicit thread counts 1 and 2
- single-CPU-affinity smoke test for the `available_parallelism() == 1` path

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9df52257dedb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.