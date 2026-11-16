# Issue

**Title:** Update `slice_sample` in `dplyr_methods.R`

## Description

Hello, this PR clears the warning in `slice_sample`. I would be grateful if you could review the code.
Related to: 

```
> data(pbmc_small)
> pbmc_small |> slice_sample(n=0)
Error: No cells found
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c7cde679bd5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.