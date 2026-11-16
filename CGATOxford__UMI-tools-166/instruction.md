# Issue

**Title:** {ts} add osx travis

## Description

Adds OS X testing to travis

The purpose is to test installation on OS X. Therefore travis testing only includes installation and then running each tool with `--help`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d2a49bb8d56b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.