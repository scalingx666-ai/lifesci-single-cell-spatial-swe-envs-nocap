# Issue

**Title:** Add release GitHub action

## Description

## New

Adds CI jobs to create new releases.

@WeilerP 2 things need to be done:
- [ ] creating a `pypi-release` [environment on GitHub](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment)
- [ ] adding the [trusted publisher on PyPI](https://docs.pypi.org/trusted-publishers/adding-a-publisher/)

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d89ca6aecbe9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.