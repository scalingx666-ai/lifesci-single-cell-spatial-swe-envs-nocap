# Issue

**Title:** add cloud storage support for annotations

## Description

This PR is a re-codification of #2501, resolving a number of issues with that PR.  Many thanks to @arogozhnikov for the idea and draft PR.

**Reviewers:**
Functional:  @seve 
Readability:  @seve 

---

## Changes
* Port gene set and label annotation read/write routes to use DataLocator and the underlying fsspec package.
* In support of this, add a couple of new API surfaces to DataLocator
* Incorporate a couple of minor bug fixes noted in the original PR (eg, missing argument in annotations.py:write_gene_sets()) 
* Reformatting to current conventions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `002c9a5c7fa5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.