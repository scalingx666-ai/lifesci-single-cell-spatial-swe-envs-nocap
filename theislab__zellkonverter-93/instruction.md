# Issue

**Title:** read dimnames correctly when using 'native' input

## Description

- in dataframe, the attribute "_index" provides the column name that will be used for the row- or column names; the column name does not have to be "_index" https://anndata.readthedocs.io/en/latest/fileformat-prose.html#dataframe-specification-v0-2-0

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `45944104d2a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.