# Issue

**Title:** {is} prepare for rsem

## Description

Add new command that allows UMI-tools output to be used with tools that expect pairs to be adjacent to each other in the output, such as RSEM and salmon.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `115404ad3335`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.