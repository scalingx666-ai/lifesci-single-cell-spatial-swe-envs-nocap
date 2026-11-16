# Issue

**Title:** [r] Fix iterative peak merging for isolated peaks

## Description

## Context

This PR fixes an edge case in `merge_peaks_iterative()` where the implementation could return too few peaks compared with the ArchR-style iterative overlap procedure it documents. The previous implementation used `range_overlaps(peaks, peaks)` to initialize keepers, but that overlap table includes self-overlaps. As a result, peaks with no real overlaps were not included in the initial keeper set. The loop also stopped once no overlap edges remained, so peaks that became isolated after a higher-priority neighboring peak discarded their only overlap were dropped instead of being retained on the next iteration.

A minimal example is a three-peak chain ordered by priority:

```r
tibble::tibble(
  chr = "chr1",
  start = as.integer(1:3),
  end = start + 2L
)
```

With half-open ranges, peak 1 overlaps peak 2, peak 2 overlaps peak 3, and peak 1 does not overlap peak 3. The iterative ArchR-style result should keep peaks 1 and 3. The previous BPCells implementation kept only peak 1 because peak 3 became isolated after peak 2 was discarded and the loop then terminated. Fully non-overlapping peak sets were also dropped.

## Changes

- Track the remaining candidate peaks explicitly during iterative merging.
- Keep all remaining peaks when no overlap edges remain.
- Preserve the existing behavior that lower input row numbers have higher priority and output rows are returned in input order.
- Add regression tests for already isolated peaks and peaks that become isolated after an iterative discard.

## Testing

Focused ATAC utility tests:

```r
testthat::test_file("tests/testthat/test-atac_utils.R")
```

Result: 67 passed, 1 skipped (`macs2` not installed).

Full test suite:

```r
testthat::test_dir("tests/testthat")
```

Result: 1984 passed, 19 skipped, 2 failed.

The failures were existing HDF5 gzip write tests outside this change:

- `test-fragment_io.R:107`: failed creating dataset `cell_names`.
- `test-matrix_io.R:168`: failed creating dataset `col_names`.

## Disclosure

GPT-5.5 was utilized to help investigate the issue and draft this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28759cdd5125`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.