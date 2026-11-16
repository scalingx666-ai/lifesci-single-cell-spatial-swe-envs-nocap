# Issue

**Title:** Keep error logs

## Description

`souporcell_pipeline.py` captures STDERR streams to `.err` files but then deletes many of these, making troubleshooting difficult.

This PR simply deletes the lines that delete the `.err` files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6872d8803eeb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.