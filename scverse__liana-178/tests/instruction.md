# Issue

**Title:** Made changes to liana code to update for decoupler-py 2.o

## Description

- main changes were in `adata_to_views`
    - decoupler-py 2.0 changes filtering to be explicit, took the same approach
    - by default `adata_to_views` does not filter samples or genes
    - arguments can be passed to `dc.pp.pseudobulk`, `dc.pp.filter_samples`, `dc.pp.filter_by_expr`, and `dc.pp.filter_by_prop` through dictionaries
- took care of changes in  decoupler API in the docs
     - **Was not able to regenerate docs** because of difficult environment definition

- decoupler 2.0 removes the weighted sum method
    - `estimate_metalinks` depends on run_wmean
    **- I did not update this function and it will fail if used**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e0c86b15cc27`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.