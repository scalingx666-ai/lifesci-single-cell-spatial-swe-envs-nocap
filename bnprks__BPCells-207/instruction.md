# Issue

**Title:** [r] Function examples for matrix ops

## Description

NOTE:  This PR targets `ia/test-data` for the sole purpose of cleaning up the diff.  It would make sense to merge `ia/test-data` into master first, and move the target of this PR to master once that is done.

Created examples for many functions in the `Matrix operations` tab in the reference. 
The ones that were left out were:

- `sctransform_pearson()`: I'm aware of how to use the function given your docs, tests, and some of the issues, but I don't think I completely get the intuition of how to show the best way to utilize it without Seurat.  I think you are in a better position to write an example for this.
- `regress_out()`: Similar reasoning to above
- All of the `IterableMatrix` methods functions:  I think these should be a separate PR

Styling wise, I tried to utilize smaller matrices when they made sense as to not take up too much compute. However, I did use `get_demo_mat()` in `marker_features()` as I felt it illustrated the functionality a little bit better.  I tried to seperate examples for examples sitting within the same `.Rd`, using some line sep and a line indicating the function being showcased.  

Nothing too fancy in terms of parameterization usage.  I think this should be the way to go until we have at least a single example for every function for CRAN.  Then we can flesh out where we deem it is needed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16faeade0a26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.