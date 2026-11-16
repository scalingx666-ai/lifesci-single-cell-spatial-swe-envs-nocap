# Issue

**Title:** spatialData deprecation and missing 'outs/' directory

## Description

Hi @lcolladotor , this pull request has 2 updates:

- Deprecation of `spatialData` in the latest version of `SpatialExperiment` (version 1.5.2). We have moved the contents of `spatialData` into `colData` for new objects built with SPE version 1.5.2 onwards, so it is best if we update `spatialLIBD` to access `colData` instead of `spatialData` (e.g. for `in_tissue` and other similar columns). We have ensured backward compatibility in SPE so the `spatialData()` accessor still works for earlier objects, so existing analysis code should still work, but new objects built with SPE version 1.5.2 onwards will no longer have anything in `spatialData`.

- Missing `outs/` directories in vignette. We had some earlier changes a few months ago regarding whether or not the `outs/` directory needs to be manually added when loading 10x Genomics Visium objects. When I ran checks there were some problems in one of the vignettes due to this, so these updates fix this and the checks pass again.

The main reason for this pull request is so that we can deploy shiny apps with SPE objects built with SPE version 1.5.2 onwards.

Note this only affects Bioc-devel, not Bioc-release.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aef4910aecb3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.