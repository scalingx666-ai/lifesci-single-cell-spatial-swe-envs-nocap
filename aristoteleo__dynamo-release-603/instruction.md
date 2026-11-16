# Issue

**Title:** Debug convert2symbol

## Description

Bug description: When we query the information from `mygene`, the output won't contain the "notfound" column if all genes can be found in the `mygene` database. This will raise a KeyError.

Solution: When "notfound" is not in the output, use all indices as the `valid_ind`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e8ffe4a103e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.