# Issue

**Title:** Fix SCT recorrection after subsetting

## Description

## Summary

This PR fixes an edge case in `PrepSCTFindMarkers()` when an SCT assay is subset to cells whose observed median UMI is lower than the correction depth stored in every SCT model.

Previously, the function skipped re-correction when all stored model median UMIs were *greater than* the newly observed minimum:

```r
all(model_median_umis > min_median_umi)
```

As a result, the stored model depths remained unchanged, and `FindMarkers()` subsequently rejected the object because its SCT models had unequal library sizes.

The skip condition now requires every stored model depth to be *equal to* the current minimum observed median UMI. This preserves the intended fast path for an object that has already been prepared at the correct depth, while ensuring a subset with a lower target depth is re-corrected.

## Testing

Added a regression test that:

- subsets a merged SCT object to low-UMI cells from each model;
- verifies the stored correction depths are initially above the subset's observed target;
- confirms `PrepSCTFindMarkers()` updates every model to the new target;
- confirms `FindMarkers()` runs successfully afterward; and
- confirms a second preparation at the same depth takes the unchanged-depth skip path without changing corrected counts.

This focused change is extracted from the broader work in #10488 / #10468.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afcae73bdf18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.