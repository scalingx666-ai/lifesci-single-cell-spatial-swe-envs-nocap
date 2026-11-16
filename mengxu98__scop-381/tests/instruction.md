# Issue

**Title:** fix: correct GSEA negative correlation label

## Description

Corrects the misspelled "Negtively correlated" annotation in GSEAPlot to "Negatively correlated" and adds a regression test for the label. Validation: targeted testthat test passed; package load passed; local R CMD check completed with 0 errors, with only pre-existing CellRank/Rd warnings and note. The required dependency and unstated-example-dependency checks both reported OK.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f8108a91040d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.