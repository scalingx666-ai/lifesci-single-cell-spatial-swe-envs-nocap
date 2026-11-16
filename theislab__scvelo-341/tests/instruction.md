# Issue

**Title:** Switch to GitHub Actions to run CI

## Description

## Changes

This PR implements the switch from Travis to GitHub Actions to run the CI. The CI is
triggered by pushs and pull requests to either `master` or `develop`.
The jobs `init`, `linting` and `test` are run consecutively:

* `init` determines whether or not to skip the CI.

* `linting` checks if the code style is according to `black` rules and
if `README.rst` can be converted into HTML.

* `test` runs the unit tests.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a42491e74061`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.