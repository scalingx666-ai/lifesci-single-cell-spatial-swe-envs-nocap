# Issue

**Title:** Fix float16 support [#2379]

## Description

Convert to float32 on startup unless backed, in which case error. 
scipy does not support complex slicing from float16 data so this is the easiest fix for now.

#### Reviewers
**Functional:** 

**Readability:** 

---

## Changes
- add
- remove
- modify

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ceb0cc6f2782`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.