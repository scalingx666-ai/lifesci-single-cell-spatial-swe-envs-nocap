# Issue

**Title:** [FE: fix #2371] fix for when labels are null

## Description

#### Reviewers
**Functional:** 
@bkmartinjr 

**Readability:** 
@seve 

---

## Changes
Check for null before reading length property of display label. Nulls are possible because Obs categoricals can have nulls

Before: ![Screen Shot 2021-10-04 at 12 38 37 PM](https://user-images.githubusercontent.com/4804047/135914050-384b92bb-b9f4-4df0-820f-19ab604c535e.png)
After: ![Screen Shot 2021-10-04 at 12 37 55 PM](https://user-images.githubusercontent.com/4804047/135913984-f427912f-302e-4cbc-8d1a-21c1515a735c.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b091d888d17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.