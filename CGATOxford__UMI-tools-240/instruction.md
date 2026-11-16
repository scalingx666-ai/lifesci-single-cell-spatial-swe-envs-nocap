# Issue

**Title:** Update count_tab.py

## Description

From the Subread Users Guide:

"When CORE format is specified, a tab-delimited file will be generated for each input file. Name of each generated file is the input file name added with ‘.featureCounts’. Each generated file contains four columns including read name, status (assigned or the reason if not assigned), number of targets and target list. A target is a feature or a meta-feature. Items in the target lists is separated by comma. If a read is not assigned, its number of targets will be set as -1."

Hence, column for target (i.e. gene id) must be $4 instead of $3.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3c90b8fddaf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.