# Issue

**Title:** Create synthAcquisition wrapper of dataAcquisition

## Description

Also removed redundant param useTFIDF from dataAcquisition (use
normalize=“TFIDF” instead).

Note that pandas.DataFrame.to_csv always writes the DataFrame’s index
as a additional column in the csv.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d83f9ba985f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.