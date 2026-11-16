# Issue

**Title:** Automated template update from cookiecutter-scverse

## Description

A new version of the scverse cookiecutter template got released. This PR
adds all new changes to your repository and helps to to stay in sync with the latest
best-practice template maintained by the scverse team.

If a merge conflict arised, a `.rej` file with the rejected patch is generated. You'll need to
manually merge these changes.

For more information about the template sync, please refer to the [template documentation](TODO).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2bd67488ad83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.