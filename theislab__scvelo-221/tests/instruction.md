# Issue

**Title:** Feat/pre commit hook

## Description

Add pre-commit hooks including code style `black` for now. In the future, further linting steps, such as flake8 for example, can be added.

This is mostly the same as #218 but does not include any code refactoring with `black`.

To ensure a meaningful output of git blame, the file `.git-blame-ignore-revs` is added. Running `git blame SOME_FILE.py --ignore-revs-file .git-blame-ignore-revs` will exclude any commits listed (specified by commit identifier) in `.git-blame-ignore-revs`. Thus, refactoring commit which do not add any new content can be excluded. This requires a Git version of at least 2.23.

FYI @VolkerBergen: I added two of your recent refactoring commits I found.

The CI has been updated to include two stages: `linting` and `test`. The former checks if the black code style is met and is currently allowed to fail to not slow down rapid development. This should be changed in the future once the entire code has been refactored to code style `black`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca39c29306ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.