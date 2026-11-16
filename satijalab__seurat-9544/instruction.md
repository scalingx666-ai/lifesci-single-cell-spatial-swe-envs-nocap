# Issue

**Title:** Fix/sketch data features docstring

## Description

Includes the `features` parameter in the docstring for the `SketchData` function. Currently, the missing documentation is causing the following WARNING to be thrown during CRAN checks:

```
❯ checking Rd \usage sections ... WARNING
  Undocumented arguments in Rd file 'SketchData.Rd'
    ‘features’
```

This warning also causes the [check-package](https://github.com/satijalab/seurat/actions/runs/12279192633/job/34262641364?pr=9538) workflow to fail. Once this PR is out of draft, we can update the branch rules for `develop` to require jobs to succeed for PRs to be merged.

Relates to:
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `775487491cbf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.