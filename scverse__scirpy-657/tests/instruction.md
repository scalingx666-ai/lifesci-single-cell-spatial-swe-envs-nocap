# Issue

**Title:** Fix KeyError being thrown when passing a mudata object to pl.clonotype_imbalance()

## Description

When passing a mudata object to pl.clonotype_imbalance() a "KeyError: '{key_added}'" is thrown.
Making sure adata is only accessed through the datahandler fixes this.


- [x] CHANGELOG.md updated
- [ ] Tests added (For bug fixes or new features)
- [ ] Tutorial updated (if necessary)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9778bf19e2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.