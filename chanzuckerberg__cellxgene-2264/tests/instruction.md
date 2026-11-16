# Issue

**Title:** fix: reset gene set colorScale on gene set deletion

## Description

#### Reviewers
**Functional:** @colinmegill 

---

## Changes
- add
* Check color accessor on gene set deletion and reset accordingly

----

#2231

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5007d307a233`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.