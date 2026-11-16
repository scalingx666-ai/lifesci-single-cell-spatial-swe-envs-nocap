# Issue

**Title:** Revamp CI checks

## Description

This PR introduces basic CI checks for `Seurat`. The implementation uses a Docker-based GitHub Action, nearly identical to the one added for `SeuratObject` in:

- 

For more details on the underlying Docker image see:

- 

The workflow:
- Pulls and starts the latest `satijalab/seurat-ci` image from DockerHub. 
- Installs all dependencies for `Seurat`.
- Runs CRAN checks with `rcmdcheck` (tests are skipped).
- Runs all tests for `Seurat` via `testthat::test_local`

---

**The workflow is currently failing, which is expected.** I will follow up soon with fixes for:

```
❯ checking Rd \usage sections ... WARNING
  Undocumented arguments in Rd file 'SketchData.Rd'
    ‘features’
```

and

```
❯ checking R code for possible problems ... [40s/40s] NOTE
  RunSLSI.StdAssay: no visible binding for global variable ‘npcs’
  Undefined global functions or variables:
    npcs
```

Once the WARNING is resolved I will update the branch rules for `develop` to require that the `Integration Checks: check-package` job passes for PRs to be merged. We'll still need to review the output of the check manually to make sure that no problematic NOTES are being thrown.

It looks like the `enrichR` package was recently removed from CRAN, which is causing the following NOTE:

```
❯ checking CRAN incoming feasibility ... [10s/73s] NOTE
  Maintainer: ‘Rahul Satija <seurat@nygenome.org>’
  
  Version contains large components (5.1.0.9007)
  
  Suggests or Enhances not in mainstream repositories:
    BPCells, enrichR, presto
  Availability using Additional_repositories specification:
    BPCells   yes   https://bnprks.r-universe.dev/   
    presto    yes   https://satijalab.r-universe.dev/
    enrichR    no   ?
```

The package’s author is aware of the —a  has been merged—and they’ve  that they’ll be re-submitting to CRAN soon. However, until that happens, we'll be blocked from cutting our own release. 

---

This PR also:
- Applies some housekeeping changes to the package's DESCRIPTION, namely:
  - Adds the `` and `` packages as suggested dependencies.
  - Adds the "BuildManual" field and sets its value to `true`.
  - Sorts all dependencies alphabetically
  - Re-orders the file to group related fields. 
- Incorporates @roi-meir's fix from #9349 to get the AppVeyor pipeline back up and running.
- Drops files relating to the defunct Travis CI and Azure pipelines—I will remove the relevant webhook shortly. 

We'll temporarily leave the AppVeyor pipeline in place so that we can compare their outputs. The new pipeline should be stricter than the old, but we might as well verify this over the next few PRs we merge. Eventually, I'll push a follow-up change dropping the AppVeyor pipeline as well. 

I've made similar DESCRIPTION updates for `SeuratObject`, for more details see:
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b703806c20a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.