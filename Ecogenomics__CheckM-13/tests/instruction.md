# Issue

**Title:** first stab at bin_union

## Description

Hmm, I modified DATA_CONFIG, and it wasn't ignored and I `commit -a`'d. Seems .gitignore doesn't actually ignore changes. Perhaps a solution like this?
http://stackoverflow.com/questions/1396617/committing-machine-specific-configuration-files

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6bc213025153`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.