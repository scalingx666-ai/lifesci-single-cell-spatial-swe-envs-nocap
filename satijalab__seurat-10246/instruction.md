# Issue

**Title:** Fix UMAP package versioning issue

## Description

# Issues

The following issues have been reported at:
- 

## Issue 1

RunUMAP relies on the UMAP package (https://github.com/lmcinnes/umap), which has its version determined by the base R utils function numeric_version(). This function cannot parse any version names with letters in them, which the latest UMAP release has: 

```{R}
> reticulate::py_run_string("import umap; print(umap.__version__)") 
0.5.9.post2
```

This results in the following error when trying to use RunUMAP:

```{R}
Error: invalid version specification ‘0.5.9.post2’
```

This fix addresses this issue by simply parsing the version to remove any versioning other than the major/minor/patch version numbers before calling numeric_version(). With this fix, RunUMAP should work with newer release versionings for the UMAP package.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `806f17695cdf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.