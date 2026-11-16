# Issue

**Title:** Update triggers for Integration Checks after default branch change

## Description

This PR adds `main` as a push & PR trigger for the `Integration Checks` workflow, replacing `develop` and `master`. Relates to:

- 

Now that the repository's default branch is also the main integration branch, it should be a lot easier to roll out changes to `.github/` like:

-  🚀 

This PR also does what  and  both failed to do—it drops the AppVeyor CI pipeline 🥳 In addition to disabling the relevant webhook, I also had to suspend/remove the AppVeyor app for the `satijalab` organization.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5c0a2665e26e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.