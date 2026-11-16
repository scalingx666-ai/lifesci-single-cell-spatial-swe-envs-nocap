# Issue

**Title:** Introduce miscellaneous CI refinements

## Description

Similar to  this PR introduces a bunch of refinements to the current CI workflow(s):

1. Refactors `Integration Checks` into `Pre-Merge Checks`
- Updates the workflow triggers to include pushes and pull requests against all `release/*` branches
- Allows the workflow to be run manually via the [Actions](https://github.com/satijalab/seurat-object/actions) tab
- Renames the name job from `check-package` to `check-package (r2u)` to better differentiate it from jobs in new workflows described below

2. Introduces `Pre-Release Checks`
- Used [r-lib/actions](https://github.com/r-lib/actions) to run checks for the package against `R-release`, `R-devel` and `R-oldrel`.
- The action is triggered by pushes and pull requests against all `release/*` branches
- The action can also be triggered manually

3. Introduces `Reverse Dependency Checks`
- Uses the [r-devel/recheck](https://github.com/r-devel/recheck) action to run reverse dependency checks
- The action must be triggered manually

4. Updates the PR template to avoid mentioning the `develop` branch. 

5. Drops the no-response.yml (deprecated/nonfunctional)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95ed7691a253`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.