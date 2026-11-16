# Issue

**Title:** {ts} debug skip count unassigned

## Description

Adds `--assigned-tag` option to ensures that the correct tag is parsed to identify reads without a gene assignment (#191)

And ensures genes which are an empty string are skipped (#273)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e757f8889b08`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.