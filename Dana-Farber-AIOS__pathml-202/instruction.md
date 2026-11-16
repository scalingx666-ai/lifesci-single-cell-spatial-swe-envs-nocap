# Issue

**Title:** Fix continuous integration configuration

## Description

This changes the CI suite to be triggered not only on pull requests, but also on pushes. 

Currently, when a PR is opened to merge branch A into dev, the CI suite is run on branch A (triggered by pull request) but when we merge it into dev, the CI suite is not actually run on the newly updated dev branch. This is causing #201, #168, and also some problems with codecoverage integration. Hopefully this will fix those by triggering the CI suite on push events (i.e., after merging has occurred).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58cbfd368c4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.