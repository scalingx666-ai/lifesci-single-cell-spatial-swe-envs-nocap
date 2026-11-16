# Issue

**Title:** Codecov

## Description

- Add codecov to workflow
- Debug existing tests

PS:
- Now the codecov report can be found [here](https://app.codecov.io/github/aristoteleo/dynamo-release).
- Python 3.7 is removed in tests because it requires certain packages to be downgraded.
- Existing tests have been debugged and passed the check. However, many tests themselves are not helpful enough. They will be refactored in the future.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fba189a0accc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.