# Issue

**Title:** Tweaks to publish action

## Description

After some discussion, we decided not to automate the initial deployment to PyPI, so I set the public action to manual trigger. To be enabled later when we aren't so concerned about testing first. Also, restricted publish to semantic versioning tags (when we re-enable it).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2a4b9dec0276`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.