# Issue

**Title:** [r] Fix `gene_score_weights_archr()` when blacklisting removes all tiles

## Description

## Context

Part of #344 (proposed PR 1). `gene_score_weights_archr()`, and so `gene_score_archr()`, errors in two blacklist cases:

- When the last genes have all of their tiles blacklisted, the weight matrix was sized from the largest gene index that kept a tile. It then had fewer rows than gene names, and assigning the row names failed.
- When the blacklist overlaps no tiles, including an empty blacklist, `tiles[-integer(0), ]` dropped every tile.

```r
genes <- tibble::tibble(
  chr = "chr1", start = c(10000, 300000, 600000), end = start + 2000,
  strand = "+", gene_id = c("gene1", "gene2", "gene3")
)
chromosome_sizes <- tibble::tibble(chr = "chr1", start = 0, end = 1e6)

# All tiles of gene3 blacklisted
gene_score_weights_archr(genes, chromosome_sizes, tibble::tibble(chr = "chr1", start = 450000, end = 1e6))
#> Error: length of Dimnames[[1]] (3) is not equal to Dim[1] (2)

# A blacklist that overlaps no tiles (an empty blacklist gives the same error)
gene_score_weights_archr(genes, chromosome_sizes, tibble::tibble(chr = "chr1", start = 999500, end = 1e6))
#> Error: invalid 'dims'
```

## Changes

- Size the weight matrix with one row per gene, so genes without retained tiles get an all-zero row.
- Filter blacklisted tiles with a logical mask, which keeps every tile when nothing overlaps.
- Add a regression test for both cases that also checks the other genes' weights are unchanged.
- Add a NEWS entry.

## Testing

Full test suite, every file in `tests/testthat` with `testthat::test_file()` (R 4.5.3, Linux): 146 tests and 2,872 expectations, no failures. The new test errors on `main` with the two errors shown above.

## Disclosure

Claude Code was used to help investigate the issue and draft this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef4ea49e9407`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.