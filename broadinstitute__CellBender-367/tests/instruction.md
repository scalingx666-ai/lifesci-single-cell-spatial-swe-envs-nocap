# Issue

**Title:** Azurize CellBender to run on ToA

## Description

We don't have GPU access in ToA and we want to run Multiome (with CellBender) on Azure. 

`cellbender_remove_background_azure.wdl` is a copy of `cellbender_remove_background.wdl` without the CUDA options for CellBender

Azurized CellBender so that it runs in Multiome by (1) removing the `--cuda` option as a CellBender input parameter and (2) removing runtime variables for GPU access when on Azure.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f3c88656aaae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.