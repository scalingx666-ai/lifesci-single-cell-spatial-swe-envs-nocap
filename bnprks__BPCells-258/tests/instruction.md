# Issue

**Title:** Update docs for commit: Use `int32_t` and `int64_t` for 10x H5 writing function

## Description

commit 9176069ab9f285c7d8fc64b6bf52d88f160e74d6
Author: Yuchen Li <105353386+ycli1995@users.noreply.github.com>
Date:   Thu May 15 06:58:35 2025 +0800

    Use `int32_t` and `int64_t` for 10x H5 writing function (#256)

    * [cpp]Force `create10xFeatureMatrix` to use `int64_t`

    * [cpp]Force "indices" to be `int32_t` in `create10xFeatureMatrix`

    * [r] Add tests for 10x hdf5 storage types

    * [cpp] Adjust 10x indices to int64_t

    * [docs] Update NEWS

    ---------

    Co-authored-by: Ben Parks <bnprks+git@gmail.com>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a6f4534652b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.