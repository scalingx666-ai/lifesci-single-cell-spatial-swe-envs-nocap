# Issue

**Title:** {ts} whitelist filter pos errors

## Description

- Adds options to whitelist to detect putative errors in the CBs above the knee threshols
- Adds tests to cover new options

See (#138) for motivation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f9b0f06309e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.