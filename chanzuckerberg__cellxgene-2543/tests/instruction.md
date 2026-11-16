# Issue

**Title:** fix embedding selection

## Description

#2535 

#### Reviewers
**Functional:** 
@roaga 

**Readability:** 

---

## Changes
reverted code to previous implementation that was presumably changed due to
"destructuring assignment" lint error; explicitly ignoring that error now

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06da05eb9fd6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.