# Issue

**Title:** Multiply multi-covariate assignment factors

## Description

Hey guys, I found a bug in the core assignment algorithm when Harmony uses multiple covariates.

`update_R()` currently adds the selected donor, chemistry, and other covariate factors. The update is exponential in summed log penalties, so those factors must be multiplied.

Adding a covariate with `theta=0` can therefore change assignments, even though the documentation says it must be neutral.

The fix is four lines and leaves the one-covariate calculation unchanged. In the reproducer below, the current code moves one cluster assignment by about 22 percentage points.

## Problem

On parent commit `df19af2`, `update_R()` adds the selected diversity factors when `vars_use` contains multiple covariates.

The factor matrix is `K x B`, and `Phicells` is `B x cells_in_block`. Each cell has one nonzero level per covariate.

For one covariate, matrix multiplication selects one factor. For multiple covariates, it adds the selected factors:

```text
factor_1 + factor_2 + ... + factor_C
```

Holding `O` and `E` fixed for the current block, the existing surrogate assignment update is exponential in per-covariate log penalties. Therefore, the product implied by the existing frozen-count update is:

```text
exp(sum(log(factor_c))) = product(factor_c)
```

The complete update does not exactly optimize the recorded objective. It freezes `O` and `E` for each block and omits derivative terms.

Column normalization does not remove the difference. Addition and multiplication produce different cluster ratios.

### A disabled covariate must be neutral

The package documentation states that `theta=0` does not encourage diversity. A disabled covariate therefore has factor `1`.

```text
parent sum:          active_factor + 1
frozen-count product: active_factor * 1
```

Thus, the parent sum can change assignments when a disabled covariate is added. The frozen-count product leaves the assignment formula unchanged.

The parent implementation matches the sum in the [Harmony2 preprint, equation FD6](https://pmc.ncbi.nlm.nih.gov/articles/PMC13015565/#FD6). However, both conflict with the additive log-penalty algebra and documented `theta=0` neutrality.

I used 48 synthetic cells, three clusters, and two covariates: donor and chemistry. Both covariates use `theta=2`.

The reproduction injects `E` and `O` to unit-test the factor-composition kernel. These matrices isolate the operation and do not represent a complete optimizer trajectory.

The reproduction compares the C++ result with an independent product formula. A natural-state regression on the bundled `cell_lines_small` PCs also checks that adding `cell_type` with `theta=0` leaves assignments unchanged.

| Check                    | Parent `df19af2` | Patched `181663c` |
| ------------------------ | ---------------: | ----------------: |
| Maximum assignment error |      `0.2187626` |         `3.67e-7` |

For the cell with the largest parent error, the cluster assignments are:

```text
parent implementation: 0.0011954, 0.3179290, 0.6808756
implied product:        0.0009541, 0.5366916, 0.4623543
```

The largest cluster assignment moves by approximately 22 percentage points in one update.

<details>
<summary>Kernel reproduction with injected counts</summary>

```r
library(harmony)
library(Matrix)

cell <- seq_len(48)
z <- rbind(
    cos(cell / 3), sin(cell / 3),
    cos(cell / 7), sin(cell / 7)
)
meta <- data.frame(
    donor = factor(rep(c("d1", "d2"), each = 24)),
    chemistry = factor(rep(rep(c("v2", "v3"), each = 12), 2))
)

run_update <- function(values, theta, E, O) {
    phi <- Reduce(rbind, lapply(values, function(x) {
        Matrix::t(Matrix::sparse.model.matrix(~0 + x))
    }))
    B_vec <- vapply(values, nlevels, integer(1))
    level_theta <- rep(theta, times = B_vec)

    set.seed(11)
    obj <- methods::new(harmony:::harmony)
    obj$setup(
        z, phi, rep(0.3, 3), level_theta,
        -1, 0.2, 1L, -Inf, -Inf, 3L, 1,
        B_vec, 1e-5, FALSE
    )
    obj$init_cluster_cpp()
    base_R <- obj$R
    obj$E <- obj$E + E
    obj$O <- obj$O + O
    obj$cluster_cpp()

    list(
        R = obj$R,
        base_R = base_R,
        phi = phi,
        B_vec = B_vec,
        theta = level_theta
    )
}

index <- matrix(seq_len(12), nrow = 3)
E <- 0.5 + index / 5
O <- 0.25 + ((7 * index) %% 11) / 3
result <- run_update(meta, c(2, 2), E, O)

level_factor <- sweep(
    (2 * E + 1) / (O + E + 1),
    2,
    result$theta,
    "^"
)
block_end <- cumsum(result$B_vec)
block_start <- c(1, utils::head(block_end, -1) + 1)
selected <- Map(function(first, last) {
    rows <- seq.int(first, last)
    as.matrix(
        level_factor[, rows, drop = FALSE] %*%
            result$phi[rows, , drop = FALSE]
    )
}, block_start, block_end)

implied <- result$base_R * Reduce(`*`, selected)
implied <- sweep(implied, 2, colSums(implied), "/")
max(abs(result$R - implied))
```

</details>

## Fix

The patch calculates the diversity-factor matrix once per block. This calculation occurs after the code removes the block cells from `E` and `O`.

The code visits each nonzero entry in the covariate design. It multiplies the matching factor into that cell assignment.

This change intentionally changes multi-covariate assignments. The one-covariate algebra remains the same, but the current patch changes its execution path.

The diff does not modify the stabilized ratio, `theta`, centroids, ridge correction, or recorded objective code.

The diff also preserves block partitioning and the removal and reinsertion of block counts.

The natural-state regression runs with `dataset` active, then adds `cell_type` with `theta=0`. With identical seeds, the parent code changes assignments by up to `0.113392`. This PR changes them by `0`.

`R CMD check --no-manual --timings` completes with status `OK`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df19af23ae06`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.