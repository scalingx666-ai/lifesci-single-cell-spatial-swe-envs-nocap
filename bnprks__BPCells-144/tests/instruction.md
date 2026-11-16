# Issue

**Title:** [r] add automatic website building

## Description

Creates a PR to html-docs whenever something is pushed to `main`, and performs the website building workflow indicated in `Wiki/Tool Development Workflows`
Title of PR is `Update docs for commit: <most_recent_commit_message>`

Message of PR is the git log of the most recent commit.  I am open to changing this to something that better describes the changes to documentation.
Example of how this would look can be found .  This PR was created as a result of pushing this commit into my personal BPCells main branch.


We can also make it perform an automatic push to `html-docs`, if that is preferred.  We can also set this up to be a manually triggered workflow.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c039d0701669`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.