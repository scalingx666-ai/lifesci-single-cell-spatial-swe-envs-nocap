# Issue

**Title:** Update github actions

## Description

This commit updates the GitHub actions workflow. Resolved `BiocCheck` errors in the workflow by adding examples in the exported functions. One error remains regarding watched tags in the local `BiocCheck` as follows.
```
$checkWatchedTag
$checkWatchedTag[[1]]
[1] "* ERROR: Maintainer must add package name to Watched Tags on the support site; Edit your Support Site User Profile to add Watched Tags."
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69eecf873eaa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.