# Issue

**Title:** respect `matrix_type` when coerced into matrix

## Description

``` r
library(BPCells)
mock_matrix <- function(ngenes, ncells) {
    cell.means <- 2^stats::runif(ngenes, 2, 10)
    cell.disp <- 100 / cell.means + 0.5
    cell.data <- matrix(stats::rnbinom(ngenes * ncells,
        mu = cell.means,
        size = 1 / cell.disp
    ), ncol = ncells)
    rownames(cell.data) <- sprintf("Gene_%s", formatC(seq_len(ngenes),
        width = 4, flag = 0
    ))
    colnames(cell.data) <- sprintf("Cell_%s", formatC(seq_len(ncells),
        width = 3, flag = 0
    ))
    cell.data
}
tmpdir <- tempdir()
mat <- mock_matrix(30, 20)
path <- normalizePath(tempfile(tmpdir = tmpdir), mustWork = FALSE)
obj <- write_matrix_dir(mat = as(mat, "dgCMatrix"), dir = path)
#> Warning: Matrix compression performs poorly with non-integers.
#> • Consider calling convert_matrix_type if a compressed integer matrix is intended.
#> This message is displayed once every 8 hours.
storage.mode(as.matrix(obj))
#> Warning: Converting to a dense matrix may use excessive memory
#> This message is displayed once every 8 hours.
#> [1] "double"
obj <- convert_matrix_type(obj, "uint32_t")
storage.mode(as.matrix(obj))
#> [1] "integer"
```

<sup>Created on 2024-03-02 with [reprex v2.0.2](https://reprex.tidyverse.org)</sup>
~                                                                                    
~                                                                                    
~                                                                                    
~

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `919983d1c223`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.