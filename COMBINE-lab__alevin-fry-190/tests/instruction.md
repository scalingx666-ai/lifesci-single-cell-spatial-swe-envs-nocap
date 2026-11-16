# Issue

**Title:** perf(quant): bound output batches and stream bootstrap summaries

## Description

Quantification now batches matrix entries across cells before taking the output lock, and streams bootstrap mean/variance matrices with bounded memory. Barcode and feature records are formatted outside their shared lock. The change also restores matrix bounds validation and propagates input/output errors after draining and joining workers.

This is stacked on the unmerged #189. Its original streaming commit is retained; the independent follow-up is . The earlier review is .

- Each worker stages at most 256 KiB plus one matrix entry per active output, including when a single cell is larger than the threshold. Shared matrix and auxiliary writers use explicit 256 KiB buffers, and header patches stay buffered.
- Bootstrap mean/variance output no longer accumulates complete triplet vectors; existing calculations and output-file conventions are preserved.
- Removed the unused remaining-cell atomic and multimapping-rate vector/mutex, stale triplet-capacity estimate, and duplicate equivalence-class key allocation.
- Returned write failures stop further quantification while workers drain queued input; all workers join before an error returns. Reader/final-flush errors propagate too. The quant CLI preserves error context instead of panicking.

Validation: 79 tests passed. Three ignored entries comprise one pre-existing ignored test and two subprocess helpers exercised by the new error-path tests. Coverage includes exact barcode/gene values across workers, bounded batches, empty/fractional/USA output, deterministic bootstrap statistics in both modes, and output/seek/flush/poisoned-lock/truncated-input failures. Formatting and diff checks pass.

Real mouse Flex bootstrap runs also passed in both output modes: all four primary matrices matched exactly (6,716 groups, 75,098 nonzeros). Bootstrap structures and numerical invariants passed; stochastic bootstrap values were not compared for exact equality.

Complete real-data verification passed for all three builds on all three datasets: every coordinate and finite f32 value was parsed, bounds and duplicate coordinates checked, and canonical per-cell SHA256 fingerprints compared after aligning barcode and gene identity. All 833,403,726 Flex counts, all 22,341,318 dense PBMC counts, and all 5,573,896 mostly-tiny-droplet PBMC counts matched. Complete feature records and normalized metadata matched too. Linux and macOS CI builds/tests, linting, and sample runs are green.

Release-build medians over three rotating-order runs at 16 threads on an AMD EPYC 9575F host, using warmed local filesystem caches. These measure quantification only. Tracing and verification ran separately from timing.

| Dataset | PR base | PR #189 | This change |
|---|---:|---:|---:|
| Human PBMC, 4,784 groups / 22.3M nonzeros | 3.69 s | 2.33 s | 2.28 s |
| Human PBMC, 73,151 groups / 5.57M nonzeros | 1.04 s | 0.75 s | 0.68 s |
| Human Flex, 2,423,889 groups / 833.4M nonzeros | 99.84 s | 24.36 s | 21.28 s |

On the large Flex experiment, the follow-up reduces median wall time by **12.6% versus #189**. The older base varies substantially (68.69–110.19 s); #189 spans 23.23–24.45 s and this change 20.71–21.80 s. The dense PBMC difference is small, while the mostly-tiny-droplet PBMC workload improves by about 9%.

Median peak RSS:

| Dataset | PR base | PR #189 | This change |
|---|---:|---:|---:|
| Human PBMC, 4,784 groups / 22.3M nonzeros | 1.959 GiB | 1.286 GiB | 1.325 GiB |
| Human PBMC, 73,151 groups / 5.57M nonzeros | 1.122 GiB | 1.040 GiB | 1.038 GiB |
| Human Flex, 2,423,889 groups / 833.4M nonzeros | 35.912 GiB | 0.625 GiB | 0.603 GiB |

The large memory reduction comes from #189's removal of whole-matrix triplets. The additional changes preserve that benefit and extend streaming to bootstrap output.

Actual count-matrix write syscalls, measured separately with `strace`:

| Dataset | PR #189 | This change |
|---|---:|---:|
| Human PBMC, 4,784 groups / 22.3M nonzeros | 4,798 | 1,080 |
| Human PBMC, 73,151 groups / 5.57M nonzeros | 2,537 | 273 |
| Human Flex, 2,423,889 groups / 833.4M nonzeros | 354,360 | 46,795 |

For Flex this is **86.8% fewer matrix writes**. Feature-file writes fall from 15,630 to 490, and barcode-file writes from 6,809 to 213. The streamed count matrix performs one seek per run. Flex base was not traced; its performance and memory were measured in the same three-way timing experiment.

The Flex input is real paired-end sequencing data (37.4 GB collated RAD, 1.87 billion mapped records), not a replicated stress fixture. Its 2.42M rows are retained barcode/sample groups across 384 sample groups; 88.5% take the tiny-cell path, so the row count should not be interpreted as that many high-quality biological cells. PBMC input sizes are 9.2 GB and 2.3 GB. The runs used `-r cr-like` and the original matching gene maps; both PBMC datasets use USA mode. No cold-cache or remote-filesystem performance claim is made.

This draft remains stacked on #189 so its author can apply the independent follow-up commit or the two changes can be reviewed together.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afa67499c595`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.