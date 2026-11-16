# Issue

**Title:** use AnnotationDbi::select

## Description

Other packages also define a function called `select`

```
dplyr
MASS
AnnotationDbi
```

It's necessary to specify the correct function to avoid conflicts.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `504986379e4c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.