# Issue

**Title:** Fix TranslationProblem and xy being set when alpha is 1 then improve tests

## Description

I did thes things in this PR:
- Fix and test 
- Add another error case for  i.e. throw error when xy is given and alpha is 1
- Test that these fail when they have to

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6cc22154caa9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.