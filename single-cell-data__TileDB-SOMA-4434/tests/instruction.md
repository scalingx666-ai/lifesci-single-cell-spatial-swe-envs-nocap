# Issue

**Title:** [ci] Update github actions

## Description

**Issue and/or context:** Towards SOMA-892

**Changes:**
* Update the actions used for GitHub workflows.
* Fix missing shapely dependency that use to be indirectly included through somacore.

Note: The "TileDB-SOMA Docker build" failures are existing failures and will be addressed in a separate PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c2aadcc26ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.