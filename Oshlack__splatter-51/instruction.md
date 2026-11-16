# Issue

**Title:** Fix bug in reversing directions for factors less than one

## Description

This fixes a bug where the lognormal multipliers don't faithfully reflect `de.downProb`.

Problem statement:

In the deleted excerpt, `dir.selected[facs.selected < 1 & dir.selected == 1] <- -1` acts on the entries converted in the previous step, `dir.selected[facs.selected < 1 & dir.selected == -1] <- 1`. As a result, there will be, on average, more multipliers greater than 1 than those less than 1 than expected for any given `de.downProb`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2ec058b989f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.