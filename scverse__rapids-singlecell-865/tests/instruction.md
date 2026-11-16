# Issue

**Title:** Harmony: faster correction with several batch keys

## Description

Speeds up `harmony_integrate` with several batch keys. Two commits on top of #830:

1. **Float32 solve with float64 refinement.** The per-cluster ridge systems were factored in float64. Equilibrated to a unit diagonal, their condition number is bounded by the ridge's share of the diagonal, so a float32 Cholesky plus refinement steps counted from that bound (`_refinement_steps`: none or one with the dynamic ridge, a few with a fixed one, the float64 solve where they would cost more or a factorization fails) gives the same accuracy.
2. **Per-level sums instead of joint-category tables.** The exact sums, right-hand sides and applied coefficients were formed per joint category (J ≈ 630k for three 100-level keys), which cost most of the time on such designs. The right-hand sides are now exact per-level sums of all keys in one pass (`segment_rtz` emits each segment's partial to several groupings), the Gram comes from the int64 joint counts scattered into the cross blocks, and the correction is applied in one pass with each segment's coefficients summed over the keys (`apply_rows` with several tables). Cluster chunks are bound by the solver's buffers alone.

Results stay bitwise reproducible and identical for any number of GPUs; they differ in the last bits from `main` (different rounding of the sums, float32 solve). One-key paths are bit-identical to `main`.

### Speed (RTX PRO 6000 Blackwell, 1 GPU, 10 Harmony iterations, median of 2 warm runs)

| design | 0.18.1 | main | this PR |
|---|---|---|---|
| 1M cells, 50 PCs, 100 clusters, keys 100 × 3 levels | 0.47 s | 0.12 s | 0.12 s |
| 1M, keys 300 × 300 | 1.15 s | 1.10 s | 0.38 s |
| 1M, keys 100 × 100 × 100 (630k joint categories) | 7.7 s | 25.3 s | 1.8 s |
| 1M, keys 1000 × 1000 | 8.0 s | 25.9 s | 5.0 s |
| 11.4M-cell atlas, 3 real keys | 4.03 s | 0.66 s | 0.67 s |
| 2M, one key with 100 levels | – | 0.150 s | 0.152 s (same bits) |
| 2M, one key with 300 levels | – | 1.09 s | 1.11 s (same bits) |
| 2M, one key, bfloat16 assignments | – | 0.135 s | 0.136 s (same bits) |

### Testing

- `tests/test_harmony.py`, `test_harmony_kernels.py`, `test_multi_gpu_utils.py` on the final tree: 2 GPUs 443 passed / 12 skipped (twice), 1 GPU 389 passed / 66 skipped.
- Same bits on 1 GPU, 2 GPUs and 3 ranks (`test_harmony_several_ranks_match_one`, now also through the float64 solve at a rank offset) and in the A/B above (`devices=[0]` vs `[0, 1]`).
- The third commit fixes a lifetime hazard the larger allreduce exposed: in pieces mode the other GPUs' summed pieces landed in the caller's buffer by peer copy, and a GPU that did not read that buffer afterwards freed it while the copy was in flight (sticky launch failure, once a GPU reset). They now land in the receive slot and a kernel moves them, so any caller may free in stream order.
- New: the dense-design test covers a 320-level design with thousands of joint categories and a nine-key design (sums and corrections in passes of eight keys); `test_harmony_rhs_bounds_per_level` checks the per-level bounds against the one-key bounds of each level's cells, past float64's range and across a split.
- A max-effort review found that indexing the new `Groupings`/`Tables` kernel parameters with a runtime loop had given the segment and apply kernels local stack frames (spills in the register-capped tile shapes, also on the one-key paths). The kernels now resolve each segment's rows and groups once per CTA into shared memory as integers, forming the pointers from the parameters, and the static bytes count towards the shared-memory opt-in (a second review caught that plans filling the 48 KB default exactly, such as 64 PCs with 64 clusters, had stopped launching; `test_harmony_shared_memory_boundary` covers those shapes). `cuobjdump` shows the frames back at 0 for the common variants, the bits are unchanged, and the one-key shapes above are within 1–2% of main.
- nvcc 12.2 (cu12 wheels) compiles the modules for sm_75–sm_90.
- rsc-ci: [pipeline 77743496](https://gitlab-master.nvidia.com/nvomics/rsc-ci/-/pipelines/77743496) (internal) on this head: all 14 configurations green, the multi-GPU H100 job included (four jobs needed a retry for infrastructure reasons: S3 downloads of the example dataset, a Slurm node failure, a cleanup-step DNS error and a node with faulting peer access; every Harmony test passed on the first attempt of each).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f0fd643438a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.