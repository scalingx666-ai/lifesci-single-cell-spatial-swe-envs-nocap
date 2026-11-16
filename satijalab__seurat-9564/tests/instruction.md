# Issue

**Title:** Add master as trigger for Integration-Checks

## Description

Picking up where #9538 left off, this PR:
1. ~~Drops the AppVeyor CI pipeline by removing the `appveyor.yml` file, per my the plan laid out ~~
2. Adds `master` as a push & PR trigger for the `Integration-Checks` workflow. Eventually, we'll be transitioning the repo over to using `main` and I wasn't initially sure if that would happen before or after the upcoming release, but now I'm sure it'll be in the new year.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `746f872d8dc7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.