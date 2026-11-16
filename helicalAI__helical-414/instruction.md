# Issue

**Title:** Fix Dependabot assignee login for Brian

## Description

## What
Correct the Dependabot assignee login for Brian from `BrianNejati` to `briannejati`.

## Why
The previous value did not match Brian's actual GitHub login (`briannejati`), so Dependabot could not assign PRs correctly. Verified via the GitHub API that `briannejati` is the valid login.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `308d908a1fd9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.