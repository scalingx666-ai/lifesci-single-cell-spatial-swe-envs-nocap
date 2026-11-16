# Issue

**Title:** [r/ci] Replace P3M Bioc Mirror

## Description

P3M's Bioc mirror is down and hasn't been restored; remove the part of `setup-r/action.yaml` that configures the P3M Bioc mirror and use the default mirror instead

Fixes [SOMA-678](https://linear.app/tiledb/issue/SOMA-678/rci-replace-p3m-bioc-mirror)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e486ab11f533`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.