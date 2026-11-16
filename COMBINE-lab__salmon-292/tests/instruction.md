# Issue

**Title:** Refactor .travis.yml.

## Description

Hi,

I did refactoring for `.travis.yml`.
This pull-request is for develop branch.

* Aligned with 2 spaces indent.
* Removed tailing space.
* Removed old commended out lines on bottom area.
  We can check past modification with `git log -p .travis.yml`.
  So, I think we can remove the comment lines.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `093b5a98e16c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.