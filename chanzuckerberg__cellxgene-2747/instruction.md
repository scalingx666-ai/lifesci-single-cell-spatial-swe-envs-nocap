# Issue

**Title:** chore: replace deprecated codecov with GitHub Action

## Description

Migrate from the deprecated codecov npm package and bash uploader to the official codecov/codecov-action@v5. This fixes gcov errors on macOS runners and provides better reliability for coverage uploads.

#### Reviewers
**Functional:** 

**Readability:** 

---

## Changes
- add
- remove
- modify

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ac256fc8b33`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.