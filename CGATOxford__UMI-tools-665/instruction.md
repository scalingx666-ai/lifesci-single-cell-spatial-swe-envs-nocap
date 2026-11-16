# Issue

**Title:** Add workflow to push releases to pypi

## Description

This GitHub workflow will push new GH releases automatically to pypi. One caveat is that the pypi API key needs to be stored in the repository or organisation secrets (under Settings) as `PYPI_API_TOKEN`. 

Relates to issue #663

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee39b777ee69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.