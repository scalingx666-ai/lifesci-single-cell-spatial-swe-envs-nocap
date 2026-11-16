# Issue

**Title:** Bug fix for WDL using MTX input

## Description

Instead of using `input_file_unfiltered` as the cellbender `--input` argument directly, it checks whether it is an MTX file. The `--input` remains `input_file_unfiltered` unless the input is an MTX file, in which case it becomes the directory name `$(dirname ~{input_file_unfiltered})`.

This obeys cellbender's current expectation that an MTX format input is to be specified by passing a directory as `--input`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `02dd763fdb3b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.