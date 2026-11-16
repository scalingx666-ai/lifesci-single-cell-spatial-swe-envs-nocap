# Issue

**Title:** Fix CRAN NOTEs

## Description

This is a quick PR to silence a couple of NOTEs currently being thrown by CRAN checks (i.e., during [Pre-Merge Checks](https://github.com/satijalab/seurat/actions/workflows/merge_checks.yaml)):

```
❯ checking CRAN incoming feasibility ... [11s/87s] NOTE
  Maintainer: ‘Rahul Satija <seurat@nygenome.org>’
  
  Version contains large components (5.2.99.9013)
  
  Suggests or Enhances not in mainstream repositories:
    BPCells, presto
  Availability using Additional_repositories specification:
    BPCells   yes   https://bnprks.r-universe.dev   
    presto    yes   https://satijalab.r-universe.dev
  
  Found the following (possibly) invalid URLs:
    URL: https://dl.acm.org/doi/10.1145/3019[134](https://github.com/satijalab/seurat/actions/runs/14593717255/job/40934561994#step:5:135)
      From: man/LeverageScore.Rd
      Status: 403
      Message: Forbidden
    URL: https://dl.acm.org/doi/abs/10.1145/3019134
      From: man/CountSketch.Rd
      Status: 403
      Message: Forbidden

❯ checking S3 generic/method consistency ... NOTE
  Apparent methods for exported generics not registered:
    AddModuleScore.Assay
  See section ‘Registering S3 methods’ in the ‘Writing R Extensions’
  manual.
  ```

The latter NOTE is from a typo introduced in:
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe616eef790f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.