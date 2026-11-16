# Issue

**Title:** Fix command to EB to use the artifact.zip file during deployment instead of the source code in the directory.

## Description

### Reviewers

**Functional:** @seve 

---

### Changes

#### Modifications

- Revert code to check if artifact.zip is in the config.yml file because we need to specify in config.yml to use artifact.zip instead of the source code in the directory, the latter of which is the default behavior of `eb deploy`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b60d20eb2f43`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.