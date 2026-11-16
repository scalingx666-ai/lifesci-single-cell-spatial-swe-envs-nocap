# Issue

**Title:** Install flexmix 2.3-13 for Travis build.

## Description

A follow-up PR to handle the consequences of PR #56 (that you noted in ):

I hadn't realized that `install.packages` only installs the latest version of a CRAN pacakge even though a maximum version is specified (e.g. see the SO question [R doesn't respect maximum version when installing package dependencies](https://stackoverflow.com/questions/42684736/r-doesnt-respect-maximum-version-when-installing-package-dependencies)). Thus if a user doesn't already have flexmix installed, the installation will fail because the latest version of flexmix does not satisfy the dependency requirement. This is why the Travis build [failed](https://travis-ci.org/hms-dbmi/scde/jobs/346440262#L5267) with the following error:

> Package required and available but unsuitable version: ‘flexmix’

Overall this early failure is a good thing because users will know something is wrong from the beginning instead of finding out later when trying to run the code.

I attempted to fix the Travis build by installing flexmix 2.3-13 before the build starts.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b67594ae6fe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.