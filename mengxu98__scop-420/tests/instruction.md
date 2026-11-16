# Issue

**Title:** fix: keep SCENIC RSS rank labels readable and axis titles centred

## Description

Long regulon lists labelled every fifth rank, so the `rss_rank` x-axis collapsed into an unreadable row of numbers (61 labels at 300 regulons). The label step now widens with the number of regulons and stays a multiple of five.

The collected axis titles are also centred on the whole figure instead of the panel grid, and the assembled object stays a patchwork so `print()`, `ggsave()` and `patchworkGrob()` keep working.

Adds a regression test for the label step in `tests/testthat/test-scenic-plot.R`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9a7d3b685134`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.