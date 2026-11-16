# Issue

**Title:** Fix documentation

## Description

Use sphinx autoapi to generate the documentation statically, without needing to import everything. Hopefully this fixes problems with readthedocs compilation.

Also update readme with installation instructions

Opening a PR to master branch so that readthedocs website will update. No changes to code so should be safe.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc3325443fb7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.