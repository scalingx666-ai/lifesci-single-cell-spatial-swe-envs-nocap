# Issue

**Title:** Fix categorical (factor) handling in native R reader

## Description

When I try to use the native R reader on an h5ad file I have, like so:

```
sce <- readH5AD("/path/to/my/anndata.h5ad", 
                reader='R',
                use_hdf5=TRUE,
                verbose=TRUE)
```

I get the following warning:
```
Warning messages:
1: In value[[3L]](cond) : setting 'colData' failed for
  '/path/to/my/anndata.h5ad':
  cannot coerce class "list" to a DataFrame
2: In value[[3L]](cond) : setting 'rowData' failed for
  '/path/to/my/anndata.h5ad':
  cannot coerce class "list" to a DataFrame
```

And the `colData` and `rowData` of the returned SCE are empty.

Tracking it down, it's because zellkonverter was unable to convert some Categorical (factor) columns in the obs/var. It's because AnnData 0.8 changed the way Categoricals are encoded.

This updates the native R reader so it can read factors encoded with the newer format. After applying this patch I was able to read my h5ad file.

EDIT:

Related: 

Thought I should also add why I'm using the R reader rather than the recommended python reader. It's because the python reader had errors reading X/layers matrices from my h5ad file due to unsorted indptr (seems to be the same issue as ). I was able to fix some of the errors by calling `sort_indices()` and resaving the AnnData, but some matrices still wouldn't load, and the ones that did were loaded as dgCMatrix instead of DelayedArray. By contrast I found the R reader successfully read all matrices from my h5ad file as DelayedArray.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa22a4490eb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.