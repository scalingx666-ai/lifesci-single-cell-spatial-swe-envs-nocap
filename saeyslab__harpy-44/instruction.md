# Issue

**Title:** Sc 19 bounding box query

## Description

Support for bounding box query

`sp.utils.bounding_box_query`. 

Necessary, because spatialdata `bounding_box_query` did not allow for query wrt multiple coordinate systems that also allowed for filtering tables layer. 
Also points layer was pulled in memory via a compute in spatialdata.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1fc1bfcce1b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.