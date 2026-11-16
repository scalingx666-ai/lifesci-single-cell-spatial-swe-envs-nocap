# Issue

**Title:** Update pre-merge workflow file to cache dependencies

## Description

### Let CI checks run faster by using cached dependencies if available

- Use [`setup-r-dependencies@v2`](https://github.com/r-lib/actions/tree/v2/setup-r-dependencies) action to install and cache dependencies, and update all steps for compatibility with this strategy. 
- Remove PDF manual build/check from the R CMD check step.

This setup assumes the `seurat-ci` Docker image is set up with the ability to install from CRAN + Bioconductor and has already pre-installed packages that are hosted elsewhere (R-universe). ()

More info: the [cache key is derived](https://github.com/r-lib/actions/blob/465b7d8e732ca3921382b1674c59bada9cbf3399/setup-r-dependencies/action.yaml#L221-L222) from the runner OS/version, R version and architecture, cache version, and the hash of `.github/pkg.lock`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9db57c26f93c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.