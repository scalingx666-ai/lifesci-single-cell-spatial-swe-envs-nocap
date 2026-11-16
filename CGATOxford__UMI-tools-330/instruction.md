# Issue

**Title:** {ts} output filtered reads

## Description

Do not merge until #328 is resolved. 

This branch adds options to write out reads filtered in `extract` to separate files for manual inspection. Calls to a `extract_methods.ExtractFilterAndUpdate()` object which result in a read not being fully processed generate a return value of `None`. This branch simply adds lines to write out the read(s) before the next call.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e0358003ae85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.