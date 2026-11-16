# Issue

**Title:** feat: frontend geneset validation

## Description

#### Reviewers
**Functional:** @colinmegill 

**Readability:** @Bento007 

---

## Changes
- add
  - Verify gene is present in var index when adding to gene set
  - Don't allow gene sets to have invalid names

----
#2160

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8b1d0dd9eb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.