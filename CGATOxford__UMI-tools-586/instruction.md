# Issue

**Title:** Fix lack of help messages in 1.1.4

## Description

remove regression that caused umi_tools.py to quit before calling the command if --help was specified.

Added a test to test that there is help output from dedup. The reference will include the version number, which means this test will go out of date every time there is a version bump. On the other hand, should we test the help message from all tools?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d98ebace3a09`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.