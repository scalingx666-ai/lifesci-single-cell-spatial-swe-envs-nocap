# Issue

**Title:** Feature/replace akima aspline

## Description

Related to this issue: 

* Replaced `akima::aspline()` with `stats::spline(..., method = "natural")`
* Removed `akima` from `DESCRIPTION`
* I don't see any other reference to `akima` in the package

I'm making a PR against the master branch. Naturally, feel free to change this branch. 

Also, this obviously doesn't affect the Bioconductor package, which is where the package is downloaded via CRAN.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0d83ad05f67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.