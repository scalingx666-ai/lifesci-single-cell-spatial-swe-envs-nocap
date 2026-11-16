# Issue

**Title:** perf: use bounded libradicl multi-barcode collator

## Description

## Summary

- delegate multi-barcode RAD collation to the new bounded `libradicl` engine
- replace the legacy `two-round`/`fast` implementations with one optimized path
- add a human-readable `--memory-limit` and retain `--max-records` and `--collation-mode` as compatibility aliases
- enforce the collator's minimum of two requested threads
- keep logical buckets sample-homogeneous so manifest `chunk_start`/`num_chunks` ranges remain physically contiguous
- add integration coverage for physical sample ordering and manifest boundaries

This is stacked on COMBINE-lab/libradicl branch `perf/optimize-multi-barcode-collation`; the dependency is pinned to commit `08ae416` so CI can test the pair. It should return to the crates.io dependency after the corresponding libradicl release.

## Flex v2 benchmark

Input: `/scratch1/rob/flex_bench/inv/flex-t32/af_map/map.rad` (39.9 GB), `-t 32 --memory-limit 1GiB`.

| implementation | wall time | scatter | gather | peak RSS |
| --- | ---: | ---: | ---: | ---: |
| previous collator | 39.47 s | ~27.0 s | — | ~1.32 GiB |
| optimized collator | 22.55 s | 9.32 s | 7.41 s | 1.04 GiB |

This is a 1.75x end-to-end speedup (42.9% lower wall time), while also reducing temporary open-file demand from roughly one descriptor per logical bucket to one spool per scatter worker.

The sample-contiguity barrier costs about 0.41 s in gather (median 7.38 s versus 6.97 s in a controlled unordered build), with no measurable whole-command regression (22.55 s ordered versus 22.76 s unordered).

## Validation

- `cargo test --all-targets` (including 7 active multi-barcode integration tests)
- `cargo clippy --all-targets -- -D warnings`
- full output audit: 2,423,889 chunks, exactly 17 physical sample ranges, exact manifest boundaries and per-sample chunk/record counts
- verified `--threads 1` is rejected by the CLI

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `93a2fe65c540`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.