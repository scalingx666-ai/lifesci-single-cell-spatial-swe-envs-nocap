# Issue

**Title:** Docker fixes, report fixes

## Description

Fix the docker build/push action.

Revamp and simplify the Dockerfile.  It no longer has to be based on an nvidia base image, because apparently new pytorch versions bundle everything needed for cuda.  This route is less error prone, because then pytorch cannot conflict with the nvidia base.  The image is a tiny bit smaller than with the nvidia base, but still huge.  Seems pytorch keeps getting larger, and we're on a new version now.

Get rid of old DockerfileGit (since the main dockefile now just installs from github).

Side issue:
Gets rid of `jupyter_contrib_nbextensions` as a requirement.  Due to new versions of jupyter and nbconvert, including `jupyter_contrib_nbextensions` in the install actually breaks the functionality of the code.  Very bizarre.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe2acc151311`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.