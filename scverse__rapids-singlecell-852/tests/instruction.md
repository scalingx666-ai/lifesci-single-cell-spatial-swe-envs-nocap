# Issue

**Title:** Match the guide assignment mixture model and parameters to pertpy

## Description

`assign_mixture_model` now fits the Poisson-Gaussian mixture with the same multi-start MAP-EM as pertpy (scverse/pertpy#1172) on the distinct count values of every guide in fused CUDA kernels with a block per guide and start, takes pertpy's parameters (`model`, `output_layer`, `show_progress`, `n_iter`, `n_init_seeds`, `seed` replace `max_iter`, `tol` and `posterior_threshold`) and writes the binary assignment matrix to a layer; the previous EM kernel, whose approximate single-start fit swapped the mixture components on 13 Papalexi guides and assigned every expressing cell to them, is replaced. `assign_to_max_guide` no longer densifies sparse input and `assign_by_threshold` returns a canonical matrix without stored zeros.

Agreement of per-guide thresholds and cell-guide assignments with pertpy main, with crispat's `ga_poisson_gauss` (default 500 SVI steps, and run to convergence with 5000 steps) and with the previous kernel (0.16.0), on four public screens with raw guide counts and one synthetic set:

| Dataset                                           | Cells x guides   | PR = pertpy (thresholds)   | PR = crispat converged   | PR = crispat default (500 steps)   | Previous rsc kernel = pertpy   |   Cell-guide Jaccard PR vs pertpy |   Cell-guide Jaccard previous rsc vs pertpy |
|:--------------------------------------------------|:-----------------|:---------------------------|:-------------------------|:-----------------------------------|:-------------------------------|----------------------------------:|--------------------------------------------:|
| Papalexi 2021 (ECCITE-seq, CRISPRko)              | 20,729 x 111     | 111/111                    | 109/111                  | 91/111                             | 78/111                         |                            1      |                                      0.3573 |
| Schraivogel 2020 (TAP-seq, CRISPRi)               | 21,977 x 86      | 84/86                      | 86/86                    | 85/86                              | 66/86                          |                            0.9996 |                                      0.9982 |
| Gasperini 2019 subset (high MOI, CRISPRi)         | 45,919 x 95      | 95/95                      | 94/95                    | 92/95                              | 62/95                          |                            1      |                                      0.9973 |
| Replogle 2020 exp. 6 (direct capture, dual guide) | 75,348 x 54      | 54/54                      | 54/54                    | 15/54                              | 39/54                          |                            1      |                                      0.3375 |
| Synthetic (11 regimes x 3 guides)                 | 20,000 x 33      | 33/33                      | 30/33                    | 18/33                              | 20/33                          |                            1      |                                      0.5469 |

The remaining differences to converged crispat are guides where crispat's SVI converges to a singular solution (a Gaussian collapsed onto one count value) that both pertpy and this PR reject, and one flat two-optima synthetic guide where the random prior starts differ between CuPy and JAX. Thresholds agree with pertpy main on 18,373 of 18,379 guides over these five datasets and four synthetic screens of up to 2.5M cells x 10,000 guides; the six others have a Gaussian posterior of exactly 0.5 at the threshold count, so the result depends on the rounding of the EM path, and the two Schraivogel non-targeting guides among them agree with crispat run to convergence.

Runtime of one `assign_mixture_model` call with the counts already on the GPU, first call in a fresh process and in parentheses a second call, on an RTX PRO 6000 Blackwell and a 32-core Threadripper PRO 7975WX; pertpy runs JAX on the CPU and crispat its default 500 SVI steps:

| Dataset | Cells x guides | This PR (GPU) | Previous kernel 0.16.0 (GPU) | pertpy main (CPU) | crispat (1 process) | crispat (32 processes) |
|:--|:--|--:|--:|--:|--:|--:|
| Papalexi 2021 | 20,729 x 111 | 144 ms (8 ms) | 38 ms (12 ms) | 3.90 s (112 ms) | 2 min | 6.50 s |
| Schraivogel 2020 | 21,977 x 86 | 140 ms (8 ms) | 29 ms (6 ms) | 1.99 s (73 ms) | 2 min | 5.10 s |
| Gasperini 2019 subset | 45,919 x 95 | 141 ms (8 ms) | 37 ms (13 ms) | 1.52 s (492 ms) | 2 min | 5.30 s |
| Replogle 2020 exp. 6 | 75,348 x 54 | 144 ms (12 ms) | 49 ms (26 ms) | 4.45 s (608 ms) | 2 min | 10.0 s |
| Synthetic (11 regimes) | 20,000 x 33 | 144 ms (11 ms) | 30 ms (6 ms) | 3.99 s (192 ms) | 1 min | 4.10 s |
| Synthetic, low MOI | 200,000 x 1,000 | 133 ms (15 ms) | 2.15 s (389 ms) | 6.29 s (4.41 s) | not run | not run |
| Synthetic, MOI 10 | 500,000 x 2,000 | 175 ms (39 ms) | 298 ms (167 ms) | 8.55 s (6.78 s) | not run | not run |
| Synthetic, low MOI | 1.0M x 5,000 | 151 ms (30 ms) | out of memory | 20.1 s (18.2 s) | not run | not run |
| Synthetic, genome-wide scale | 2.5M x 10,000 | 169 ms (49 ms) | out of memory | 4.03 s (2.19 s) | not run | not run |

The first call includes about 130 ms of CUDA and CuPy warm-up. The previous kernel densifies the count matrix, so it runs out of memory beyond 1M cells, and its single-digit milliseconds on small screens come from 90 approximate single-start iterations that give the wrong components on 13 Papalexi guides.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `addc04094682`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.