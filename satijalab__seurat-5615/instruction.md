# Issue

**Title:** Add misc removal to DietSeurat

## Description

Hi Seurat Team,

So I realize this is edge case but I think it's edge case with little downside to add.  This is PR to add parameter to remove the `@misc` slot when using `DietSeurat`  since the misc slot can store anything it can become quite large in size and users may want to remove easily when using `DietSeurat` to reduce object size.  I set the default to TRUE because like I said this is probably edge case where users would want to remove it so under normal circumstances it wouldn't be removed.

Thanks,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eaaf6750c8b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.