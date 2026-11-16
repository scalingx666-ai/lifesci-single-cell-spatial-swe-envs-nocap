# Issue

**Title:** fix: change scale for qc plots

## Description

@LTLA 
I realize proportion is by feature/gene? -> https://github.com/jkanche/scran.js/blob/master/src/PerCellQCMetrics_Results.h#L47

so should there be a gene selection for the proportion plot? or completely remove proportion ?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2aee69bd2289`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.