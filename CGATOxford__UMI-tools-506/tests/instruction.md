# Issue

**Title:** Fix "umi_tools command" prints stack trace

## Description

Also:
- minor refactor
- pass return value from command through to sys.exit()
- pretty error if the command is not known

(Didn't test this PR myself yet, just trying to fix my "first launch" experience of getting a stack trace)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5c2dd0fd208d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.