# Issue

**Title:** perf: use libradicl single-barcode collator

## Description

Stacked on #181 and depends on COMBINE-lab/libradicl#55.

Summary:
- route ordinary short-read single-barcode RNA collation through the new libradicl engine
- retain the existing generic implementations for positional RNA records, long-read RNA records, and ATAC
- preserve output naming, header and file tags, barcode correction, orientation filtering, unmapped-count correction, compression, and collate metadata
- pin libradicl to the reviewed single-barcode engine commit

Benchmark:
On the 11 GB 5k PBMC v3 RAD file (288,194,503 retained records, 32 requested threads, 2 GiB memory budget), alternating three-run medians improved from 6.17 s to 4.44 s: 28.0% lower wall time / 1.39x throughput. Median user CPU fell from 97.51 s to 27.05 s and median peak RSS from 1,737,720 KiB to 1,502,808 KiB. The implementation also succeeds with RLIMIT_NOFILE=128, where the former many-bucket-file design fails.

Correctness:
A semantic comparison against the existing output matched all 4,784 cell chunks and all 288,194,503 records, including UMIs and ordered packed alignments (1,437,861,514 alignments total).

Validation:
- cargo test --all-targets
- cargo clippy --all-targets -- -D warnings
- cargo fmt --all -- --check

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8c660fec59a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.