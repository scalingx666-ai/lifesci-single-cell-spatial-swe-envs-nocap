# Issue

**Title:** Fix env

## Description

Remove deepcell from environment.yml, since it was causing environment setup to hang (#195 )
Also skip tests which rely on Mesmer model if deepcell package is not installed.
This is not ideal, but it's a stopgap fix to get our CI pipeline running again until we can find a way to work around deepcell's fragile installation

While I am at it, also pin versions in environment.yml for reproducible dev/testing environments, and unpin versions from setup.py install_requires for flexible user installations

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7b3f910341a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.