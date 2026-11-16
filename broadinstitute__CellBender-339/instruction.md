# Issue

**Title:** Update cli.py to add newer Cell Ranger feature types

## Description

In Cell Ranger 7+, there is a longer list of [feature types](https://www.10xgenomics.com/support/software/cell-ranger/7.2/advanced/cr-multi-config-csv-opts#feature-types) one can specify in `cellranger multi`. These should be added to the list of allowed feature types in CellBender so they won't be rejected by `--exclude-feature-types` (the Multiplexing Capture feature is of particular note here).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `578c214e1afe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.