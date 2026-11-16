# Issue

**Title:** Accelerate barcode routing and Flex GPL counting

## Description

## Summary

- compile resolved sample corrections into one private AHash execution lookup carrying the dense sample index and exact-source flag
- replace the immutable multi-sample cell-whitelist `DashMap` view with an `AHashSet`
- aggregate cell counts in bounded per-worker AHash maps and periodically reduce them into shared histograms (65,536 combined distinct entries per worker)
- use private AHash correction and bucket maps in ATAC scatter/sort
- preserve the public `generate_permitlist_map` and related compatibility types rather than adopting the public-type changes proposed in #172

GPL still owns every correction decision. Hash iteration order cannot affect accepted targets, correction artifacts, or frequencies. libradicl only applies compiled decisions. This PR is stacked on #184 and depends on COMBINE-lab/libradicl#57.

## Flex v2 measurements

Input: `/scratch1/rob/flex_bench/inv/flex-t32/af_map/map.rad`, 32 threads, three runs per main comparison.

| Path | Median wall | Median peak RSS |
|---|---:|---:|
| Original resolved-correction GPL | 31.39 s | 1735.5 MiB |
| Fused route, SipHash | 28.80 s | 1697.9 MiB |
| Fused route, AHash | 19.43 s | 1741.5 MiB |
| + immutable AHash whitelist | 17.02 s | 1703.0 MiB |
| + bounded local counts (final) | **9.35 s** | **1550.2 MiB** |

Final versus original: **70.2% lower wall time** and **10.7% lower peak RSS**.

The no-whitelist forced-cell path improved from 15.65 s / 1402.3 MiB to 9.84 s / 1352.4 MiB (37.1% faster, 3.6% lower RSS). Cell-Frequency and sample-Frequency completed in 8.03 s and 8.14 s respectively and reproduced the pre-change correction artifacts byte-for-byte.

A direct FoldHash 0.2 comparison over six runs measured 19.22 s median versus 19.43 s for AHash at the fused-routing stage. The approximately 1% and inconsistent paired advantage did not justify a new direct dependency or fixed-seed tradeoff.

## ATAC measurement

On the local 28.4-million-record / 3.8 GB ATAC RAD, 13 paired warm-cache sort runs improved from 0.76 s to 0.72 s median (5.3%). The BED outputs are byte-identical.

## Correctness and validation

- correction plans byte-identical across all paired Flex runs
- every per-sample `permit_freq.bin` decoded to identical barcode/count mappings
- sample-Frequency produced the same routing totals and zero spill runs on this dataset
- ATAC BED SHA-256 identical between SipHash and AHash builds
- `cargo test --release --all-targets` (42 library, 2 binary, 4 ATAC, 3 infer, 9 multi-barcode; one real-data test ignored)
- `cargo clippy --all-targets -- -D warnings`
- libradicl: 71 release tests and warnings-as-errors clippy

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8afbf97305ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.