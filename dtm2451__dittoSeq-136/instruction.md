# Issue

**Title:** add 'labels.repel.adjust' input to all scatter-type plotters

## Description

Added 'labels.repel.adjust' input to 'dittoDimPlot()', 'dittoScatterPlot()', 'dittoDimHex()', and 'dittoScatterHex()'. The input allows extra control of how labels will be placed when 'do.label = TRUE' (and 'labels.repel' is not set to FALSE) by providing a mechanism to pass desired parameters through to the ggrepel function used for plotting the labels.

- [x] documentation
- [x] tests in dittoDimPlot

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d6fa57b460a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.