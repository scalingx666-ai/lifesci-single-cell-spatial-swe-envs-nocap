# Issue

**Title:** perf(em): iterate only the genes a cell can touch

## Description

## The problem

`em_optimize_subset` keeps `alphas_in` and `alphas_out` dense over every gene (every gene x status in USA mode). The M-step is already sparse: `em_update_subset` walks only the equivalence classes present in the cell. But the two loops around it were not:

```rust
for index in 0..num_alphas {          // 236,697 on the toy dataset
    if alphas_out[index] > ALPHA_CHECK_CUTOFF { ... }
    alphas_in[index] = alphas_out[index];
    alphas_out[index] = 0.0_f32;
}
```

That runs once per EM iteration, up to `MAX_ITER` = 100 iterations, for each of 26,126 cells, regardless of whether a cell has five equivalence classes or five thousand. The per-cell cost was a function of the reference size, not of the cell.

The gap is visible in the benchmark added in #169: `em_unique_only/128`, which returns before the iteration loop, took 20.6 ms for the same 128 cells that `em_optimize_subset_batch/128` took 2.43 s on.

## The change

Collect the indices a cell can touch once, before the loop, and iterate that.

The support is not simply the labels. `em_update_subset` writes only the labels of the cell's equivalence classes, but in USA mode `get_abundance_for` also *reads* the two sibling statuses of each label. An index that is read but never written still has to be reset every iteration, otherwise it keeps its initialisation value forever instead of being zeroed by the first copy, and the denominators change. Those siblings are therefore collected as well.

Initialisation is likewise restricted to the support. In the dense version the entries outside it were initialised too, but nothing reads them before the first iteration copies `alphas_out` (still zero there) over the top, so the result is unchanged. The one behavioural difference is that `EmInitType::Random` now draws one value per support entry rather than one per gene. The draws were never tied to a particular index, and no caller in this crate uses `Random` (`quant` picks `Uniform` or `Informative`, `infer` picks `Informative`).

## Measurements

Toy dataset from the `sample_run` CI job: 29.5M reads, 26,126 cells, 375,446 refs, 78,899 genes, USA mode (236,697 alphas). Apple M-series 16 cores, macOS 26.6, `rustc 1.97.1`, `-t 8`. Interleaved A/B, median of 7 repetitions, range in brackets:

| phase | before | after |
|---|---|---|
| `generate-permit-list` | 1.691 [1.67-1.72] | 1.722 [1.59-1.99] (+1.8%) |
| `collate` | 1.871 [1.85-1.96] | 1.862 [1.84-2.05] (-0.5%) |
| `quant -r cr-like` | 0.958 [0.92-1.04] | 0.942 [0.93-0.97] (-1.7%) |
| `quant -r cr-like-em --small-thresh 0` | 5.813 [5.72-6.22] | **2.153 [2.13-2.20] (-63.0%)** |

`cargo bench --bench em`, over the cells carrying the most equivalence classes, medians:

| bench | before | after |
|---|---|---|
| `em_optimize_subset_batch/16` | 339.3 ms | 105.9 ms (-69%) |
| `em_optimize_subset_batch/128` | 2.427 s | 466.7 ms (-81%) |

The microbenchmark gain is larger than the end-to-end gain because `quant` also reads the collated RAD and writes the matrix, neither of which this touches.

## Output equivalence

Bit-identical, not merely equivalent:

- same dimensions and same nonzero count, 5,099,981 both sides
- re-keying every nonzero of `quants_mat.mtx` by its barcode gives the same digest on both sides (`e00de64d...`), **0 of 26,126 cells differing**

(The re-keying is because raw file bytes differ between any two runs of this pipeline, including two runs of the same unmodified binary, since cells are emitted in thread-completion order.)

## Left alone

`run_bootstrap_subset` (`src/em.rs:433`) and `em_optimize_long_read` (`src/em.rs:852`) contain the same dense loop. Neither is exercised by the runs above, so extending the change to them would mean shipping an unmeasured claim. They are worth the same treatment in a follow-up with a workload that exercises them (`--num-bootstraps`, and a long-read RAD respectively).

## Checks

- `cargo test --workspace`: 24 passed, 1 ignored, 0 failed
- `cargo clippy --workspace --all-targets`: clean
- `cargo fmt --check`: clean

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c82c0ba8432`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.