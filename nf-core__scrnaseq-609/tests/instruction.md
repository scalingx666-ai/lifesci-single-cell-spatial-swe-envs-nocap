# Issue

**Title:** Important! Template update for nf-core/tools v4.2.2

## Description

Version `4.2.2` of [nf-core/tools](https://github.com/nf-core/tools) has just been released with updates to the nf-core template. For more details, check out the blog post: https://nf-co.re/blog/2026/tools-4_2_0

Please make sure to merge this pull-request as soon as possible, resolving any merge conflicts in the `nf-core-template-merge-4.2.2` branch (or your own fork, if you prefer). Once complete, make a new minor release of your pipeline.

For instructions on how to merge this PR, please see [the template sync documentation](https://nf-co.re/docs/developing/template-syncs/merge-automated-pull-requests).

For more information about this release of [nf-core/tools](https://github.com/nf-core/tools), please see the `v4.2.2` [release page](https://github.com/nf-core/tools/releases/tag/4.2.2).

> [!NOTE]
> Since nf-core/tools 3.5.0, older template update PRs will not be automatically closed, but will remain open in your pipeline repository. Older template PRs will be automatically closed once a newer template PR has been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6bbb2cb0f66b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.